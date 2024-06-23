---
date: 2024-06-23 10:45:30
updatedAt: 2024-06-23 10:45:48
---
![|center](Pasted%20image%2020240623104840.png)
## 1. coordinateing stage
- Elasticsearch의 모든 색인 작업은 일반적으로 document ID(routing_key)를 기반으로 라우팅을 사용해 복제 그룹을 확인함
	- `shard = hash(routing_key) % number_of_primary_shards`
- 복제 그룹이 확인되면, 그 작업은 내부적으로 그룹의 현재 기본 샤드로 전달됨
## 2. primary stage
- 기본 샤드는 작업의 유효성을 검증하고, 다른 복제본으로 전달하는 역할
- 복제본은 오프라인 상태일 수 있으므로 기본 샤드가 모든 복제본에 복제할 필요가 없음
	- 대신 Elasticsearch는 작업을 수신해야 하는 샤드 복제본 목록을 유지함
	- 이 목록을 `in-sync copies`라고 불리며, 마스터노드에서 관리됨
	- 사용자에게 승인된 모든 인덱스 및 삭제 작업을 처리했음을 보장하는 정상 샤드 복사본 직합


https://www.elastic.co/blog/found-elasticsearch-top-down
https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up
https://www.javaadvent.com/2022/12/elasticsearch-internals.html
https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-replication.html#basic-write-model