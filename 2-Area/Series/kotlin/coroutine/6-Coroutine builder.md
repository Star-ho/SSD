- suspend함수는 Continuation을 다른 suspend함수에 전달해야 함
- 일반함수에서 suspend를 호출 할 수 없음
- 어디서 suspend함수를 호출해야 하는가?
- **Coroutine builder**
- 일반세계와 suspend세계를 연결하는 다리역할


## runBlocking
- coroutine의 일반적인 규칙은 thread를 block하지 않는다 이지만, runblocking은 다른 coroutine builder와는 다르게 쓰레드를 block함
- main function과 같이, 쓰레드를 block하지마 않으면 프로세스가 종료되기 때문에 이러한 경우 runBlocking을 사용해야함
	- runBlocking은 새로운 코루틴을 실행하고, 현재 쓰레드를 코루틴이 완료될 때 까지 block함
- runBlocking인자로 Dispatcher를 전달하여 다른 쓰레드에서 runBlocking을 실행하게 할 수 있음
	- 다른쓰레드에서 runBL



https://medium.com/@wind.orca.pe/kotlin-coroutines-coroutine-builders-korean-recap-24a36300513b
https://kotlinlang.org/docs/coroutines-basics.html#an-explicit-job