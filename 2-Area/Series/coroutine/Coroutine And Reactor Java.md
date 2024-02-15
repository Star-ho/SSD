## Coroutine은 어떤 방식으로 Reactor를 지원하는가
- 아래 코드는는 org.jetbrains.kotlinx:kotlinx-coroutines-reactor의 mono\<T\>를 suspend 해서 T로 변경하는 awaitSingleOrNull함수이다
```kotlin
public suspend fun <T> Mono<T>.awaitSingleOrNull(): T? = suspendCancellableCoroutine { cont ->  
    injectCoroutineContext(cont.context).subscribe(object : Subscriber<T> {  
        private var seenValue = false  
  
        override fun onSubscribe(s: Subscription) {  
            cont.invokeOnCancellation { s.cancel() }  
            s.request(Long.MAX_VALUE)  
        }  
  
        override fun onComplete() {  
            if (!seenValue) cont.resume(null)  
        }  
  
        override fun onNext(t: T) {  
            seenValue = true  
            cont.resume(t)  
        }  
  
        override fun onError(error: Throwable) { cont.resumeWithException(error) }  
    })  
}
```
- Mono의 확장함수
- 기존에는 값을 바로 가져오려면 block()을 호출하여 데이터를 가져올 때 까지 Thread를 block시켰음
- injectCoroutineContext로 context를 주입한 후 subscribe함
- subscribe시 Subscriber를 정의함
	- onSubscribet시 continuation의 취소 핸들러를 정의함
	- onNext시 인자로 받은 값을 continuation의 resume에 인자로 호출
	- onComplete시 null을 continuation의 resume에 인자로 호출
	- onError시 인자로 받은 error를 continuation의 resumWithException에 인자로 호출

### Coroutine은 onSubscribe시 Subscriber에 동작을 추가함으로서 reactor를 지원함

## 작업
1. a에 요청 
   	- 리스폰스 A
2. b에 요청 
	- 리스폰스 B
3. a와 b를 합쳐서 -> Z요청을 만듬
4. 1요청을 c에전송해서 리스폰스 C를 받고 리턴

## Reactor java

```kotlin
val a: MONO<A>=webclient.get("a")
	.bodyToMono(A.class)

val b: MONO<B> =webclient.get("b")
	.bodyToMono(B.class)

val z:Z = Mono.zip(a,b)

val c:Mono<C> = webclient.get("c")

return c
```

### 상세
1. A에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- 리스폰스 생성

2. B에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- 리스폰스 생성

3. C를 보내기전에 reactor에서도 wait가 필요 

## coroutine

```kotlin
val a: A=webclient.get("a")
	.bodyToMono(A.class)

val b: B =webclient.get("b")
	.bodyToMono(B.class))

val z:Z = Z(a.await(),b.await())

val c:C = webclient.get("c").awaitSingle()
```
### 상세
1. A에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- subscriber는 continuation.resume()을 호출하여 해당 continuation재실행
- 리스폰스 생성

2. B에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- subscriber는 continuation.resume()을 호출하여 해당 continuation재실행
- 리스폰스 생성

- continuation 결과를 기존 로직을 실행하는 (쓰레드?)에 '전달'함

3. C를 보내기전에 reactor에서도 wait가 필요 


io dispatcher에도 selector가 있어
send만 하고 다른 클라이언트로 스위칭 하는지?



