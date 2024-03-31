---
created: 2024-03-02T22:41:32
date: 2024-03-08T23:18
updated: 2024-03-31T22:43
---
쓰레드와의 차이가 뭔지
limitedParallelism확인해보기

coroutine dispatcher 생명주기

coroutine은 하나의 쓰레드를 어떻게 나눠쓸지 생각하는것
blocking job이 있을때
현재 자바의 green쓰레드에서는 
- 쓰레드를 blocking하고 blocking이 끝나면 다음작업이 시작됨
- 멀티 쓰레드를 사용한다면 다른 쓰레드에서 blocking작업이 가능
- reactive에서도 동일, blocking작업을 다른 쓰레드에서 실행
- coroutine에서는 blocking작업 발생시 해당 쓰레드에서 context switch를 하여 다음 작업을 실행함

reactive, coroutine에서 nonblocking이 가능하려면 어차피 nonblocking io를 지원하는 라이브러리가 있어야 가능
- 하나의 요청에 여러개의 io가 발생한다면 coroutine+virtual thread가 제일 나을까?

여기서 reactive streamse랑 어떻게 호환되는지
- https://huisam.tistory.com/entry/webflux-coroutine
- await가 subscibe와 같이 동작

reactor netty에서 어떤상황에서 쓰레드가 변경되는지 확인해야함
- subscribe할때

webflux 에서 임의의 클래스에서 request정보 받아오기
- https://velog.io/@slolee/ThreadLocal-%EC%82%AC%EC%9A%A9%EC%8B%9C-%EC%A3%BC%EC%9D%98%ED%95%A0%EC%A0%90

coroutine builder
job
coroutine start
0- coroutine
# ContinuationInterceptor


- 스레드와 스케줄러 알아보기
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sthwin&logNo=221956619428


#wait-to-update 