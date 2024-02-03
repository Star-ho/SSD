- Kotlin Coroutine은 일시중단을 구현하기 위해 ContinuosPassing style을 적용하였음
```
suspend fun getUser(): User?

fun getUser(continuation: Continuation<*>): Any?
```
- 위쪽의 suspend function은 컴파일 시 아래와 같이 continuation이라는 인자를 받고, User?가 아닌 Any?타입을 반환하게 변경됨
	- continuation은 현재 코루틴의 상태를 가지고 있는 상태머신임
	- 항상 function의 마지막 인자로 추가됨
	- Any?로 바뀌는 이유는 getUser 함수가 User?도 반환하지만, suspend된다면 COROUTINE_SUSPENDED을 반환하기 때문

> 추후 kotlin에 유니온 타입이 추가된다면 User?|COROUTINE_SUSPENDED가 될 수 있음

```
suspend fun myFunction() {
  println("Before")
  delay(1000) // suspending
  println("After")
}
```

```
fun myFunction(continuation: Continuation<Unit>): Any {
    val continuation = continuation as? MyFunctionContinuation
        ?: MyFunctionContinuation(continuation)

    if (continuation.label == 0) {
        println("Before")
        continuation.label = 1
        if (delay(1000, continuation) == COROUTINE_SUSPENDED){
            return COROUTINE_SUSPENDED
        }
    }
    if (continuation.label == 1) {
        println("After")
        return Unit
    }
    error("Impossible")
}
```


https://kt.academy/article/cc-under-the-hood