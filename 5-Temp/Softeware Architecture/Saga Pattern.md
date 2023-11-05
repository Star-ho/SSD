- 이전의 이름은 LLT(Long Lived Transaction)
- 이전의 이름에서 알수 있듯이 오래 살아있는 트랜잭션을 어떻게 처리할까는 문제의 해결책임
- 마이크로서비스화 되면서 서비스별 데이터베이스를 가지고 있음
- 그리고 각각의 서비스들이 트랜잭션을 가지고 있음
- 각각의 서비스들에서 트랜잭션처리를 어떻게 관리할것인가?
	- ex) 롤백 처리를 어떻게 하는지?

## 정의 
- SAGA는 로컬 트랜잭션의 연속임
- 각각의 로컬 트랜잭션은 트랜잭션 완료후 다음 트랜잭션에 메시지를 보내거나, 이벤트를 발생시킴
- 이 과정에서 에러 발생시 보상트랜잭션을 실행하여, 이전 로컬 트랜잭션 내용을 롤백시킴
- 이를 구현하는 두가지 방법이 있음


### Choreography-based saga
![[Pasted image 20231105170101.png]]

### Orchestration-based saga
![[Pasted image 20231105170046.png]]


## 장점
- 높은 동시성


## 단점
- 낮은 일관성
	-  송금을 예로 들면, 사용자 A의 계좌에서 돈이 인출되었지만 최종적으로 송금에 실패하는 중간 상태를 볼 수 있습니다.
- 보상 트랜잭션을 추가로구현해야 하기 때문에 개발 난이도가 높음

>saga의 어원이 정확히 밝혀지지 않았음
	- 아래의 두가지 추측이 존재
		- 연결된 이벤트에 길고 자세한 이야기(문학에서 사용되는 용어)
		- Segregated Access of Global Atomicity의 약어

https://stackoverflow.com/questions/63319018/why-the-pattern-for-microservices-distributed-transactions-named-as-saga