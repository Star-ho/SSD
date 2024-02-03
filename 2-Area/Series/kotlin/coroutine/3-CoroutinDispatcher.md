- dispatcher의 사전적 정의
	- 사람이나 차량, 특히 긴급 차량을 필요한 곳으로 보낼 책임이 있는 사람
- 코루틴에서는?
	- 코루틴을 실행시킬 thread를 결정
	- 코루틴을 실행시킬 쓰레드를 제한함
	- 쓰레드 풀로 dipath하거나, unconfined한 상태로 실행할 수 있음
- coroutine builder에서는 CoroutinContext를 optional하게 받는데 여기서 dispatcher를 인자로 받을 수 있음
## Default dispatcher
- 코루틴에서 아무것도 설정하지 않는다면 기본으로 제공되는 dispatcher
- CPU-intensive한 작업을 실행하기 위해 디자인됨
- 기본 thread갯수는 최소 2개, 최대 cpu core수만큼 생성됨
	- 이론상 cpu-intensive한 작업을 하고, blocking하지 않는다고 가정하면 최적의 갯수임

## IO Dispatcher
- 파일 읽기/쓰기, 네트워크 요청과 같은 I/O작업에 사용하기 위해 만들어짐
- 코어의 수에 따라 다르지만, 최대 64개 thread를 생성
	- thread 갯수가 무제한이라면 쓰레드를 계속 생산할것이고, 쓰레드를 생성/삭제하는 것도 비용이므로 적절한 thread 수를 관리해야함

## Main dispatcher
- UI를 다루는 어플리케이션에서 사용하는거
	- ex) Android, JavaFx

> **_limitedParallelism_**
> 하나의 무거운 코루틴에서 모든 DefaultDispatcher를 사용하면 다른 코루틴에서 사용할 DefaultDispatcher가 부족할 수 있음
> limitedParallelism을 사용해서 현재 코루틴에서 사용할 쓰레드 수를 제한할 수 있음

https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-coroutine-dispatcher/
https://kt.academy/article/cc-dispatchers
https://medium.com/@wind.orca.pe/dispatchers-kotlin-coroutines-659a5681f329
https://kotlinlang.org/docs/coroutine-context-and-dispatchers.html#dispatchers-and-threads