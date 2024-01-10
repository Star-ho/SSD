# 비동기 메시징
- 결합도를 낮춰줌
	- 중간의 매개체를 통해 메시지를 전달하므로 수신자와 발신자가 서로를 몰라도 메시지 송/수신이 가능
- consumer수를 늘림으로써 가용성 확보가 가능해짐
- polling 방식일때는 consumer의 가용성에 맞춰 데이터를 소비하므로 consumer의 가용성이 증대됨
	- 중간 infra가 터질 수 있음

# 방식
## Database(Transaction Outbox Pattern)
### 구성
![Pasted image 20231105224429.png](app://df8f59cfdb2eba9748f1ed25dad91cbedcbe/Users/sungho/obsidian/SSD/real-resource-image/Pasted%20image%2020231105224429.png?1699191869128)
- 데이터베이스 테이블을 messaging box로 이용
- 해당 데이터 + 상태 로 구성됨
	- 상태는 진행예정, 진행중, 완료 등의 상태가 있음
- 2번에서 outbox를 읽는 방법으로 polling이나 cdc를 사용하는 방법이 있음
	- polling시에는 relay서버가 해당 테이블을 주기적으로 확인
	- cdc를 사용한다면, cdc를 사용해 relay서버로 request보냄
- 응답성이 낮아도 되고, relay server 1개로 부하가 감당 가능할때 사용하기 좋음
### 장점
- 거의 모든 서비스가 데이터베이스를 사용하므로 추가 인프라가 필요 없음(비용절감)
### 단점
- 다른 방식에 비해 느림
	- cdc를 사용하던 polling을 사용하던 늘미
- relay서버 증설 시 부담이 있음
	- 한테이블을 여러 서버가 읽을때 락관리를 어떻게 할것인가
		- 깔끔하게 transaction level을 SERIALIZED로 올린다?
- 인스턴스가 2개 이상이면 lock을 걸어줘야함
	- 스케일링시 부담있음

## Redis Pub-sub

![[Pasted image 20240110132820.png]]
- subscriber가 해당 channel을 구독하고 있을때, publisher가 데이터를 publish하면 구독하고 있는 모든 subscriber에게 데이터를 전달함
- subscriber가 존재하지 않는다면 따로 보관하지 않으므로 데이터는 사라짐
- 100프로 전송 보장이 되지 않아도 문제없는 케이스에서 사용하기 좋음
- 주로 채팅이나 푸쉬알림 등에 사용됨

### 장점
- 데이터를 따로 저장하지 않으므로 빠름
### 단점
- 컨슈머가 항상 해당 토픽을 확인하고 있어야하며 컨슈머가 없을시 데이터가 삭제됨


## Message queue
- 오직 하나의 컨슈머에게만 보낼 수 있음
## Message Broker
- 메시지 내용을 알 고 있음
## Streaming System(Kafka, Pulsar)
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

https://oliveyoung.tech/blog/2023-08-07/async-process-of-coupon-issuance-using-redis/BC

#argent 
#Async-messaging
#Transactional-outboxk
#message-queue 
#redis
#pub-sub
#message-broker
#Kafka 
#event-streaming