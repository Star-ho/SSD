---
date: 2024-03-02T22:41:32
updatedAt: 2024-04-21 18:34:34+8560
tags: 
---
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
		- A에 요청을 보내고 (context switching)
		- A의 결과가 오면 (context switching) B에 요청을 보내고 (context switching)
		- B의 결과가 오면 C에 요청을 보내고 (context switching)
		- C의 결과가 나오면 d를 만들어서 응답
	- coroutine일때
		- A요청을 보내고, B에 요청을 보내고, C에 요청을 보내고 결과를 기다림(context switching)후에 결과가 다 오면 d를 만들어 응답
			- thread에 비해 한번에 요청을 다 보낼 수 있다는 장점이 있음

> thread가 비동기라고 크게 다르지 않음
> reactor Java의 경우 default로 eleasticBounded 스케줄러를 사용하면
> A와 B와 C의 요청이 동시에 보내겠지만, 모두 다른 Thread에서 처리되므로 context switching이 발생
>  coroutine이라고 다를까? 어차피 DispatcherIO thread를 사용할텐데?


#eventually-update