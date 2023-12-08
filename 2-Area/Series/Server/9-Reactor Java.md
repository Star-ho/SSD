- callback보다 나은점
	- callback hell이 발생하지 않음
- Future보다 나은점
	- 더 많은 연산자를 지원함

### Backpressure
- request 메서드를 사용하여 몇개까지 처리할것인지 알려줘

### Hot Sequence vs Cold Sequence
- Hot Sequence
	- 한번 구독하면 생성된 시퀀스를 재사용함
	- 나중에 구독한 구독자는 이전꺼 시퀀스를 받지 못하고 구독이후의 시퀀스를 받을 수 있음
- Cold Sequence
	- 구독할때마다 시퀀스가 재 생성됨

## Flux

![[Pasted image 20231208223306.png]]

- Flux\<T\>는 0개에서 N개의 비동기 시퀀스 항목을 방출하는 Publisher\<T\>임
- onComplete 혹은 onError로 종료됨
- `onNext`, `onComplete`, `onError` 로 downstream을 호출할 수 있음
- 종료를 포함한 모든 이벤트는 선택사항힘
	- onNext가 없고 onComplete만 있다면 빈 유한 시퀀스임
	- onNext 있고 onComplete가 없다면 무한 시퀀스임

## Mono

![[Pasted image 20231208224210.png]]


publishOn이 뭐하는 놈인지
subscribeOn이 뭐하는 놈인지
sink가 뭐하는 놈인지
reactor upstream downstream
https://wiki.terzeron.com/Programming/Java/Reactor_Flux%EC%9D%98_publishOn_subscribeOn%EC%9D%84_%EC%9D%B4%EC%9A%A9%ED%95%9C_%EC%8A%A4%EC%BC%80%EC%A5%B4%EB%A7%81

https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sthwin&logNo=221956619428

https://godekdls.github.io/Reactor%20Core/contents/

https://devpress.csdn.net/cloudnative/62f640837e6682346618aeb5.html

https://itecnote.com/tecnote/java-threading-model-of-spring-webflux-and-reactor/

https://www.stefankreidel.io/blog/spring-webflux

https://medium.com/@akhaku/netty-data-model-threading-and-gotchas-cab820e4815a