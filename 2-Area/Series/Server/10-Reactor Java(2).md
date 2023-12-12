# Threading and Scheduler
- Flux나 Mono를 얻는다고 실행되지 않음
- 따로 지정하지 않으면 Reactor는 subscribe가 발생한 쓰레드에서 모든 연산자가 실행됨
- 따로 지정함으로써 
- Threading
	- 




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