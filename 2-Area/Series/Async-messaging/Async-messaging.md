- 비동기 메시징
- 결합도를 낮춰줌
- consumer수를 늘림으로써가용성 확보가 가능해짐

## 방식
- Database(Transaction Outbox Pattern)
	- 응답성이 낮아도 되고, 인스턴스가 1개만 있을때
- Redis Pub-sub
	- 컨슈머가 항상 붙어있어야함, 없으면 삭제됨
- Message queue
	- 오직 하나의 컨슈머에게만 보낼 수 있음
- Message Broker
	- 
- Streaming System
	- 