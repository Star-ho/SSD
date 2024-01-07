- 비동기 메시징
- 결합도를 낮춰줌
- consumer수를 늘림으로써가용성 확보가 가능해짐

## 방식
- Database(Transaction Outbox Pattern)
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