## Coroutine-Context가 쓰이는곳
- coroutine builder의 첫번째 파라미터
```
public fun CoroutineScope.launch(
   context: CoroutineContext = EmptyCoroutineContext,
   start: CoroutineStart = CoroutineStart.DEFAULT,
   block: suspend CoroutineScope.() -> Unit
): Job {
   ...
}
```
- Coroutine Scope의 인자
```
public interface CoroutineScope {
    public val coroutineContext: CoroutineContext
}
```
- Continuation의 인자
```
public interface Continuation<in T> {
    public val context: CoroutineContext
    public fun resumeWith(result: Result<T>)
}
```
- **코루틴의 대부분의 곳에 쓰이므로 매우 중요한 요소임!**

## 
```
@SinceKotlin("1.3")  
public interface CoroutineContext {  
	public operator fun <E : Element> get(key: Key<E>): E?
	
	public fun <R> fold(initial: R, operation: (R, Element) -> R): R  
	
	public operator fun plus(context: CoroutineContext): CoroutineContext{
		...
	}
    
    public interface Key<E : Element>  
  
    /**  
     * An element of the [CoroutineContext]. An element of the coroutine context is a singleton context by itself.  
     */    public interface Element : CoroutineContext {  
        /**  
         * A key of this coroutine context element.         */        public val key: Key<*>  
  
        public override operator fun <E : Element> get(key: Key<E>): E? =  
            @Suppress("UNCHECKED_CAST")  
            if (this.key == key) this as E else null  
  
        public override fun <R> fold(initial: R, operation: (R, Element) -> R): R =  
            operation(initial, this)  
  
        public override fun minusKey(key: Key<*>): CoroutineContext =  
            if (this.key == key) EmptyCoroutineContext else this  
    }  
}
```

- 해당 context의 정보를 가지고 있음
- Key와 Element를 가짐
	- 키는 해당 컨텍스트를 식별하는 키
	- Element는 Context를 상속받는 요소
		- context안에 context를 가질 수 있음
- 합치면 CombinContext가 됨
	- left에 이전의 context를 찾음




https://kt.academy/article/cc-coroutine-context