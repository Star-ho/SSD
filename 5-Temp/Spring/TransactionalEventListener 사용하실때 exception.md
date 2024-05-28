---
date: 2024-05-28 22:02:45
updatedAt: 2024-05-28 22:02:59
---
https://lenditkr.github.io/spring/transactional-event-listener/

AfterCommit 은 Async 로 돌려서 예외를 잡아야합니다

---

허재님 여기서 궁금한게 있습니다!

저희가 비즈니스 로직과 EventListener에서 다른 트랜잭션을 적용시키고 싶어서
기존에는 AfterCommit과 Propagation.REQUIRES_NEW를 사용했습니다.

그런데 Async를 사용하면 어떻게 트랜잭션 관리를 하지? 라고 생각을 했는데, 찾아보니까 트랜잭션은 쓰레드로컬로 관리된다길래 Async를 사용하면 다른 쓰레드니까 다른 트랜잭션으로 실행된다고 생각했습니다. 옳은 생각일까요?

---

뭔가 질문이 모호한 것 같아서 다시 정리해보자면, AfterCommit + Async 만 사용해도 될지, 아니면 AfterCommit + Propagation.Requires_new + Async를 사용해야 할지가 궁금했습니다

---

Async 는 스레드를 따로 따기 때문에 다른 커넥션을 씁니다
스레드단위의 DB Connection 동작 방식인 Spring Transactional 을 뛰어넘어
리스너를 두고 그안에서 다른 서비스를 인보크 하는 상황이라면 필요없고요
트랜잭셔널의 시작점도 같이 태깅하는 상황이라면
REQUIRED_NEW, NOT_SUPPORTED를 붙여줘야지만 동작하게 바뀌었습니다.
@TransactionalEventListener method must not be annotated with @Transactional unless when declared as REQUIRES_NEW or NOT_SUPPORTED
https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x#data-access-and-transactions
(예외가 터졌을시) 그리고 required_new 속성을 줘도 메인 스레드에서 함께 동작하면 그 스레드의 트랜잭션은 다 버려지게 됩니다

