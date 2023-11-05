- 이전의 이름은 LLT(Long Lived Transaction)
- 이전의 이름에서 알수 있듯이 오래 살아있는 트랜잭션을 어떻게 처리할까는 문제의 해결책임
- 마이크로서비스화 되면서 서비스별 데이터베이스를 가지고 있음
- 그리고 각각의 서비스들이 트랜잭션을 가지고 있음
- 각각의 서비스들에서 트랜잭션처리를 어떻게 관리할것인가?
	- ex) 롤백 처리를 어떻게 하는지?

- 가장



>saga의 어원이 정확히 밝혀지지 않았음
	- 아래의 두가지 추측이 존재
		- 연결된 이벤트에 길고 자세한 이야기(문학에서 사용되는 용어)
		- Segregated Access of Global Atomicity의 약어

https://stackoverflow.com/questions/63319018/why-the-pattern-for-microservices-distributed-transactions-named-as-saga