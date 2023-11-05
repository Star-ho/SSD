- msa 환경에서 도메인 서버스로 보낸 create, update, delete 이벤트는 반드시 수행되어야함
- 







Message Relay로 cdc를 사용
kafka connect도 사용할 수 있다니 확인해 볼것

### 장점
- 모든 데이터가 outbox에 저장되므로 장애가 났을때 대응이 수월함

### 단점
- 메시지를 직접 보내는 패턴보다 속도가 느릴 수 있음
	- 메시지는 필요한상황에 바로 보내기때문
	- 하지만 Transactional outbox는 중간에 Message Relay서버가 변경을 확인하고 서비스로 요청을 보낼때까지 시간이 빔
- Message Relay 서버가 추가됨으로서 관리해야 할게 하나 더 늘어남
- 한번 이상 명령이 수행될 수 있음
	- 그러므로 멱등성을 보장해야함
	- 작업마다 id를 기록해놓고 해당 id를 가직 작업이 수행되었으면 재처리 하지 않아야함

> 정보는 Transactional outbox로 저장하고 끝난후 api요청을 보내는건 어떨까?
