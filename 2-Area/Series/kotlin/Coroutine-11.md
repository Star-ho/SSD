

### CoroutineScope
- CoroutineContext를 가진다
- 가진 coroutineContext를 가지고 Scope를 만든다
- 해당 Scope를 실행시킨다
- launch와 async 확장 함수를 가지고 있다
	- launch와 async에 CoroutineContext를 따로 지정 안할경우, EmptyCoroutineContext를 가짐

### launch
- return을 job으로함
### async
- return defer로 함
- return값을 받을 수 있음


### Continuation
- 현재 상태를 저장하는 객체
- 지역변수, resume 상태등을 관리

### runBlocking
- Coroutine에서 쓰레드를 블록시키는애
- 끝날때까지 블로킹됨
- Coroutine에서는 blocking이 아닌 suspend인데 얘만 blocking임
- coroutine이 아닌세계와 coroutine밖의 세계를 연결


### job
- coroutineConext의 element 구현체중 하나

### dispatcher
- coroutine context의 구현체 중 하나
- io
	- thread를 최대 64개까지 생성
	- blocking되는 경우가 많으니 context switching하여 여러 작업 처리
- default
	- thread를 최대 코어수 최소 2개 생성
	- context switching을 줄여 cpu집약적인 일을 빠르게 처리


### CoroutineStart
- Default
- LAZY
- ATOMIC
- UNDISPATCHED