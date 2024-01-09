## 비동기 메시징
- 결합도를 낮춰줌
- consumer수를 늘림으로써 가용성 확보가 가능해짐
- polling 방식일때는 consumer의 가용성에 맞춰 데이터를 소비하므로 consumer의 가용성이 증대됨
	- 중간 infra가 터질 수 있음

## 방식
- Database(Transaction Outbox Pattern)
	- 데이터베이스 큐를 messaging box로 이용
	- 해당 데이터 + 상태 로 구성됨
		- 상태는 진행예정, 진행중, 완료 등의 상태가 있음
	- 데이터베이스 트랜잭션이 끝나고, relay서버가 해당 테이블을 확인 후 consumer에게 데이터를 전달
		- consumer에서 바로 읽을 수 있음
	- relay서버 증설 시 
	- 응답성이 낮아도 되고, 인스턴스가 1개만 있을때
	- 인스턴스가 2개 이상이면 락 관련 관리해줘야함
		- 스케일링시 부담있음
- Redis Pub-sub
	- 컨슈머가 항상 붙어있어야함, 없으면 삭제됨
- Message queue
	- 오직 하나의 컨슈머에게만 보낼 수 있음
- Message Broker
	- 메시지 내용을 알 고 있음
- Streaming System(Kafka, Pulsar)
	- 여러 컨슈머에게 보낼 수 있음
	- 메시지를 저장함

https://blog.bytebytego.com/p/why-do-we-need-a-message-queue
https://blog.iron.io/message-queue-vs-streaming/
https://dreamix.eu/insights/message-queue-vs-message-broker-whats-the-difference/
https://www.baeldung.com/pub-sub-vs-message-queues
https://www.linkedin.com/pulse/differences-between-message-queue-event-stream-frank-lieu
https://risingwave.com/blog/differences-between-messaging-queues-and-streaming-a-deep-dive/
https://www.cloudamqp.com/blog/why-is-a-database-not-the-right-tool-for-a-queue-based-system.html
https://stackoverflow.com/questions/48099098/message-broker-vs-database-and-monitoring

#argent 