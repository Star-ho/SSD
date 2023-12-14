- 2013년 어플리케이션의 요구사항(짧은 응답시간, 100%가용성)의 변화로 리액티브 시스템을 정의한 리액티브 선언문(reactive manifesto)가 작성됨 (현재 최신 버전 2014년 v2.0)

- 리액티브 선언문에서는 리액티브 시스템이란 Responsive, Resilient, Elastic, Message Driven을 가진 시스템이라고 정의

### Responsive(응답성)
- 시스템은 가능한 적시에 응답해야함
- 사용성과 유용성 때문에 중요한것도 맞지만, 문제를 신속하게 감지할수 있다는 더 중요한 장점이 있음
- 응답성이 높은 시스템은 신속하고 일관된 응답을 주는것에 중점에 두며, ***신뢰할 수 있는 상한선***을 두어 일관된 서비스 품질을 제공함
- 위와같은 일관된 행동은 오류를 간소화하고, 최종 사용자와의 신뢰를 구축하며, 더 많은 상호작용을 장려함
### Resilient(장애에 대한 내구성)
- 시스템은 장애가 발생하여도 응답성을 유지해야함
- 고 가용성의 중요한 시스템 뿐만아니라, 중요하지 않은 시스템도 포함됨
- 내구성은 복제, 격리, 위임, 고립를 통해 달성됨
	- 
### Elastic(탄력성)

### Message Driven(메시지 전달)
> aws에서 툭하면 elastic이 나오게 되는데 선언문에 나온 elasitc의 개념이다.[링크](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.concept.elasticity.en.html)  
> 리액티브 선언문을 많이 읽어보며, 어떻게 개발해야 할지 개발 방향에 좀 감을 잡은거 같다.

- 이중 jvm을 타겟으로한 비동기, 논블로킹의 표준인 reactive streams나왔고 이를 구현한 Project Reactor와 rxJava가 나왔다.

- 이중 Project Reactor와 Spring Framework가 손잡고 나온것이 Spring Webflux이다.

- 현재 Spring Webflux에서 많이 사용하는 Http Server인 Reactor Netty는 Project Reactor의 프로젝트중 하나이다


[https://www.reactivemanifesto.org/ko](https://www.reactivemanifesto.org/ko)  
[https://www.reactive-streams.org/](https://www.reactive-streams.org/)  
[https://github.com/reactor/reactor](https://github.com/reactor/reactor)

#Reactive 
#Concept 