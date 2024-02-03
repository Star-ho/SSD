- Kotlin Coroutine은 일시중단을 구현하기 위해 ContinuosPassing style을 적용하였음
```kotlin
suspend fun getUser(): User?

fun getUser(continuation: Continuation<*>): Any?
```
- 위쪽의 suspend function은 컴파일 시 아래와 같이 continuation이라는 인자를 받고, User?가 아닌 Any?타입을 반환하게 변경됨
	- continuation은 현재 코루틴의 상태를 가지고 있는 상태머신임
	- 항상 function의 마지막 인자로 추가됨
	- Any?로 바뀌는 이유는 getUser 함수가 User?도 반환하지만, suspend된다면 COROUTINE_SUSPENDED을 반환하기 때문

> 추후 kotlin에 유니온 타입이 추가된다면 User?|COROUTINE_SUSPENDED가 될 수 있음


## Suspend함수 컴파일

```kotlin
suspend fun printUser(token: String) {
  println("Before")
  val userId = getUserId(token) // suspending
  println("Got userId: $userId")
  val userName = getUserName(userId, token) // suspending
  println(User(userId, userName))
  println("After")
}
```

```kotlin
fun printUser(
    token: String,
    continuation: Continuation<*>
        ): Any {
    val continuation = continuation as? PrintUserContinuation
    ?: PrintUserContinuation(
        continuation as Continuation<Unit>,
        token
    )

    var result: Result<Any>? = continuation.result
    var userId: String? = continuation.userId
    val userName: String

    if (continuation.label == 0) {
        println("Before")
        continuation.label = 1
        val res = getUserId(token, continuation)
        if (res == COROUTINE_SUSPENDED) {
            return COROUTINE_SUSPENDED
        }
        result = Result.success(res)
    }
    if (continuation.label == 1) {
        userId = result!!.getOrThrow() as String
        println("Got userId: $userId")
        continuation.label = 2
        continuation.userId = userId
        val res = getUserName(userId, continuation)
        if (res == COROUTINE_SUSPENDED) {
            return COROUTINE_SUSPENDED
        }
        result = Result.success(res)
    }
    if (continuation.label == 2) {
        userName = result!!.getOrThrow() as String
        println(User(userId as String, userName))
        println("After")
        return Unit
    }
    error("Impossible")
}

class PrintUserContinuation(
    val completion: Continuation<Unit>,
    val token: String
) : Continuation<String> {
    override val context: CoroutineContext
    get() = completion.context

    var label = 0
    var result: Result<Any>? = null
    var userId: String? = null

    override fun resumeWith(result: Result<String>) {
        this.result = result
        val res = try {
            val r = printUser(token, this)
            if (r == COROUTINE_SUSPENDED) return
            Result.success(r as Unit)
        } catch (e: Throwable) {
            Result.failure(e)
        }
        completion.resumeWith(res)
    }
}
```
- 함수의 오퍼레이션이 변경됨
	- 마지막 인자로 continuation이 생기고, return 타입이 Any로 변경됨 
- 5번 라인, Continuation이 해당 함수의 Continuation인지 확인하고, 아니라면 생성
	- resume될떄는 해당 함수의 Continuation이므로, 처음 실행될때만 생성함

- 11,12,13번 라인, 지역변수들을 선언하고, 

- Continuation은 label을 가짐
	- label로 현재 어디까지 코드가 진행되었는지 파악하고, 다음 실행때 어디부터 시작할지 결정함

- suspend된다면, COROUTINE_SUSPENDED을 리턴 후 중단이 끝난 후 다시시작함
	- io작업이 발생한다면 작업을 끝내지 못하므로 우선 COROUTINE_SUSPENDED을 리턴함

- suspend이후 resum

https://kt.academy/article/cc-under-the-hood