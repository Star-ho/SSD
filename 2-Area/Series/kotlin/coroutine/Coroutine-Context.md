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
- 해당 context의 정보를 가지고 있음
- Key와 Element를 가짐
	- 키는 해당 컨텍스트를 식별하는 키
	- Element는 Context를 상속받는 요소
		- context안에 context를 가질 수 있음
- 합치면 CombinContext가 됨
	- left에 이전의 context를 찾음




https://kt.academy/article/cc-coroutine-context