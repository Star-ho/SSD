- Coroutine은 thread를 나눠쓰는것
- thread에서 비동기는 blocking call을 만났을때 다른 쓰레드를 실행함으로써 cpu core의 낭비를 막음
	- context switching비용 발생
- coroutine은 blocking call이 발생했을때, suspend하고 다른작업을 함

## 예시
- 작업 내용
	- A에 요청을 보내고 a응답을 받음
	- 하나의 작업이 1~100을 더함
	- a응답과 1~100을 더한것을 가지고 b요청을 만들어 B에 요청 전송
- Thread일때
	- A요청을 보내고 다른 작업을 수행함(context switching)
	- A요청이 끝나면 1~100을 더하고 결과를 가지고 b를 만들고 B에 요청 전송
- coroutine일떄
	- A요청을 보내고 1~100을 더함
		- 1~100의 결과가 나온후 A의 응답이 왔다면 b를 만들고 B에 요청 바로 전송(context switching 발생 x)
		- 1~100의 결과가 나온후 A의 응답이 오지 않았다면 suspend함(실제 아무런 동작을 하지 않으므로 context switching발생
			- 이후 A의 응답이 오면 b를 만들고 B에 요청 바로 전송(context switching 발생 x)

- 작업내용
	- A,B,C에 요청을 보내고 응답을 바탕으로 d를 만들어서 리턴
	- Thread일때
		- A요청을 보내고 (context switching)
		- B