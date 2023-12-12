# Threading and Scheduler
- Flux나 Mono를 얻는다고 실행되지 않음
- 따로 지정하지 않으면 Reactor는 subscribe가 발생한 쓰레드에서 모든 연산자가 실행됨
- Reactor가 실행되는 위치는 스케줄러에 의해 정해짐
### Schedulers.immediate()
- 직접적으로 현재 실행되고 있는 쓰레드에서 실행됨
### Schedulers.single()
- 쓰레드를 생성하여 스케줄러가 dispose될때까지 모든 호출자에 대해 동일한 쓰레드를 재사용
- 호출별 새로운 쓰레드를 생성하고 싶다면 Schedulers.newSingle()을 사용해야함
### Schedulers.elastic()
- 배압 문제를 숨기고 너무많은 쓰레드를 생성하기에 Schedulers.boundedElastic()가 도입된 이후로 잘 사용되지 않음
### Schedulers.boundedElastic()
- 필요에 따라 워커풀을 생성하고, idle한 워커풀이 있다면 재사용함
- 워커풀이 일정시간 사용되지 않으면 삭제됨(기본 60초)
- Schedulers.elastic()과 달리 워커풀 생성에 제한이 있음(기본 cpu core*\10)
- 한도에 도달한다면 최대 100,000 작업이 큐에 추가됨
- 쓰레드가 다시 재사용 될때 큐에 추가됨
	- 100,000이 넘게 추가되면 버려지는듯?
- 블로킹프로세스에 자체 쓰레드를 부여하여 다른 리소스 묶이지 않도록 할 수 있음
	- [링크](https://projectreactor.io/docs/core/release/reference/#faq.wrap-blocking)참고
### Schedulers.parallel()
- 병렬 작업에 맞게 고정된 워커풀을 생성
- CPU Core갯수만큼 워커풀을 생성함
### 추가
- `Schedulers.fromExecutorService(ExecutorService)`를 사용하여 ExecutorService를 Scheduler로 사용할 수 있음
- `newXXX`를 사용하여 다양한 스케줄러 타입의 인스턴스를 생성할 수 있음
- boundedElastic()은 single과 parallel과 다르게 피할 수 없는 legacy blocking콜을 사용하는데 
	- single과 perallel을 사용한다면 blocking api(block(), blockFirst(), blockLast())를 사용하면 IllegalStateException을 발생시킴
- 어떤 연산자는 기본으로 특정 Schduler를 사용함
	- ex) Flux.interval는 Schedulers.parallel()을 사용함
		- 변경가능함

## publishOn, subscribeOn
- Reactor에서는 Reactor chain 내에서 실행 컨택스트를 바꿀 수 있는 publishOn과 subscribeOn을 제공함
### publishOn
- 다른 오퍼레이터들과 같이 체인 내에서 적용될 수 있음
- 연관된 Scheduler의 worker에서 콜백이 실행되는 동안 업스트림에서 신호를 받아, 다운스트림으로 재생해줌
	- 따라서 후속 오퍼레이터가 실행되는 곳에 영향을 미침
- 스케줄러에서 선택된 하나의 쓰레드로 실행 컨텍스트를 변경함
- 시퀀스 내에서 onNext를 호출하면 선택된 쓰레드로 실행됨
- 이후 특정 스케줄러를 지정하지 않는 한, publishOn 이후의 연산자는 동일한 쓰레드에서 실행됨

```
Scheduler s = Schedulers.newParallel("parallel-scheduler", 4); //main thread

final Flux<String> flux = Flux 
	.range(1, 2) //
	.map(i -> 10 + i) .publishOn(s) 
	.map(i -> "value " + i); 
	
new Thread(() -> flux.subscribe(System.out::println));
```






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