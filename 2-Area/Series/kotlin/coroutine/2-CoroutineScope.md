- 새로운 coroutine에 대한 Scope를 정의함
- launch와 async와 같은 coroutine builder는 CoroutineScope의 확장함수임
- 팩토리 메서드인 CoroutineScope()와 MainScope()로 standalone CoroutineScope생성
	- 더 이상 필요가 없을때는 cancel을 사용하여 








https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-coroutine-scope/