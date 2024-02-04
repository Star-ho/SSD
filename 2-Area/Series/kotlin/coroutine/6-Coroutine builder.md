- suspend함수는 Continuation을 다른 suspend함수에 전달해야 함
- 일반함수에서 suspend를 호출 할 수 없음
- 어디서 suspend함수를 호출해야 하는가?
- **Coroutine builder**
- 일반세계와 suspend세계를 연결하는 다리역할

## runBlocking
```kotlin
@Throws(InterruptedException::class)  
public actual fun <T> runBlocking(context: CoroutineContext, block: suspend CoroutineScope.() -> T): T {  
    contract {  
        callsInPlace(block, InvocationKind.EXACTLY_ONCE)  
    }  
    val currentThread = Thread.currentThread()  
    val contextInterceptor = context[ContinuationInterceptor]  
    val eventLoop: EventLoop?  
    val newContext: CoroutineContext  
    if (contextInterceptor == null) {  
        // create or use private event loop if no dispatcher is specified  
        eventLoop = ThreadLocalEventLoop.eventLoop  
        newContext = GlobalScope.newCoroutineContext(context + eventLoop)  
    } else {  
        // See if context's interceptor is an event loop that we shall use (to support TestContext)  
        // or take an existing thread-local event loop if present to avoid blocking it (but don't create one)        
        eventLoop = (contextInterceptor as? EventLoop)?.takeIf { it.shouldBeProcessedFromContext() }  
            ?: ThreadLocalEventLoop.currentOrNull()  
        newContext = GlobalScope.newCoroutineContext(context)  
    }  
    val coroutine = BlockingCoroutine<T>(newContext, currentThread, eventLoop)  
    coroutine.start(CoroutineStart.DEFAULT, coroutine, block)  
    return coroutine.joinBlocking()  
}
```
- coroutine의 일반적인 규칙은 thread를 block하지 않는다 이지만, runblocking은 다른 coroutine builder와는 다르게 쓰레드를 block함
- main function과 같이, 쓰레드를 block하지마 않으면 프로세스가 종료되기 때문에 이러한 경우 runBlocking을 사용해야함
	- runBlocking은 새로운 코루틴을 실행하고, 현재 쓰레드를 코루틴이 완료될 때 까지 block함
- runBlocking인자로 Dispatcher를 전달하여 다른 쓰레드에서 runBlocking을 실행하게 할 수 있음
	- 다른 쓰레드에서 runBlocking을 실행해도 runBlocking을 실행한 쓰레드를 Block함
	- Dispatcher는 코루틴을 실행할 쓰레드를 선택하는 것으로, 현재 쓰레드를 block하는 것을 막을 수 없음
- CoroutineScope의 확장함수가 아님, CoroutineScope외부에서 사용 가능
	- 완료될때까지 쓰레드를 block하므로 CoroutineScope외부에서 사용하는건 권장하지 않음
	- 


## launch
- 개념적으로 새로운 쓰레드를 생성하는 것과 유사함
- 코루틴을 시작하고, 독립적으로 실행함
```kotlin
public fun CoroutineScope.launch(  
    context: CoroutineContext = EmptyCoroutineContext,  
    start: CoroutineStart = CoroutineStart.DEFAULT,  
    block: suspend CoroutineScope.() -> Unit  
): Job {  
    val newContext = newCoroutineContext(context)  
    val coroutine = if (start.isLazy)  
        LazyStandaloneCoroutine(newContext, block) else  
        StandaloneCoroutine(newContext, active = true)  
    coroutine.start(start, coroutine, block)  
    return coroutine  
}
```
- CoroutineScope의 extension function임
- coroutine context를 받아, 해당 context내에서 3번쨰 인자로 받은 block을 실행시킴

```kotlin
fun main() {  
    GlobalScope.launch {  
        delay(1000L)  
        println("World!")  
    }  
      
    GlobalScope.launch {  
        delay(1000L)  
        println("World!")  
    }
  
    println("Hello,")  
    Thread.sleep(1500L)  
}// Hello,  
// (1 sec)  
// World!  
// World!  
```
- main 함수에서 Thread.sleep()을 호출하지 않는다면, Hello만 출력됨
	- launch내의 delay는 실제로 쓰레드를 block하지 않음

## async
```kotlin
public fun <T> CoroutineScope.async(  
    context: CoroutineContext = EmptyCoroutineContext,  
    start: CoroutineStart = CoroutineStart.DEFAULT,  
    block: suspend CoroutineScope.() -> T  
): Deferred<T> {  
    val newContext = newCoroutineContext(context)  
    val coroutine = if (start.isLazy)  
        LazyDeferredCoroutine(newContext, block) else  
        DeferredCoroutine<T>(newContext, active = true)  
    coroutine.start(start, coroutine, block)  
    return coroutine  
}
```
- launch와 비슷하지만 async는 값을 Deffered로 감싸서 return함
- Deffered는 suspending method await를 가짐
- 


https://medium.com/@wind.orca.pe/kotlin-coroutines-coroutine-builders-korean-recap-24a36300513b
https://kotlinlang.org/docs/coroutines-basics.html#an-explicit-job