- 2013년 어플리케이션의 요구사항(짧은 응답시간, 100%가용성)의 변화로 리액티브 시스템을 정의한 리액티브 선언문(reactive manifesto)가 작성됨 (현재 최신 버전 2014년 v2.0)

- 리액티브 선언문에서는 리액티브 시스템이란 Responsive, Resilient, Elastic, Message Driven을 가진 시스템이라고 정의

### Responsive(응답성)
### Resilient(내구성)
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