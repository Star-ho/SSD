---
created: 2023-10-30T23:27:19
date: 2024-03-03T11:41
updated: 2024-03-31T22:43
---
형님들 스프링 관련질문이있습니다!
@TransactionalEventListener 사용시 이벤트 내부에서 에러 발생시 기본이 debug로 로그를찍는게 전부인데요
에러를 잡아서 제가원하는 형태로 에러로그를 남기는게 가능할까요?(@Async없는 경우)
어떤방법이 좋을까요? 

1. 리스너 실행시에 콜백을 실행해주는 확장 포인트가 하나보이는데
TransactionSynchronizationUtils
  invokeAfterCompletion()
TransactionalApplicationListenerSynchronization
  afterCompletion()
    processEventWithCallbacks()
리스너 생성을 new로 하고 있어서서 어느부분에서 콜백을 주입해줘야할지 어려웠습니다.
TransactionalEventListenerFactory 
-> new TransactionalApplicationListenerMethodAdapter 
-> new TransactionalApplicationListenerSynchronization

2. 템플릿패턴으로 인터페이스를 생성하고 @TransactionalEventListener 사용하던 클래스를 인터페이스 구현으로 변경한다.
요건 기존에 사용하던 코드를 모두 뜯어고쳐야했구요…

3. @Aspect, @Around를 사용하여 @TransactionalEventListener가 붙은곳에 로그를 생성한다.