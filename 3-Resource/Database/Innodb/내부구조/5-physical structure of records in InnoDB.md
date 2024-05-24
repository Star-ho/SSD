---
date: 2024-05-22 22:43:24
updatedAt: 2024-05-24 16:06:56
tags:
  - InnoDB
  - InnoDB-File-Structure
  - hugo_blog
categories:
  - Database
---
## Record
- 해당 포스트에서는 COMPACT row format만 고려함

### Record offsets
- 이전 포스트에서 레코드 오프셋은 레코드를 가르키는 구조라고 설명했음
- 레코드 오프셋은, 가변길이인 레코드 데이터 자체의 시작을 가르키지만, 각 레코드 앞에는 가변길이의 레코드 헤더가 존재함
- 해당 포스트의 글과 그림에서 레코드 데이터는 N에 존재하고, N+1과같이 양수오프셋으로 표현함
	- 헤더는 N-1과 같이 음수 오프셋으로 표현함
- InnoDB는 종종 레코드의 시작점 위치인 N을 원본으로 지칭함

### The record header
![center](Pasted%20image%2020240524152545.png#center)
- Next Record offset
	- 현재 레코드에서 페이지 내 다음 레코드의 시작점까지의 상대적 오프셋
- Record Type
	- 레코드 유형으로 일반(0), 노드 포인터(1), 최소값(2), 최상위(3)의 4가지 값만 지원됨
- Order
	- 이 레코드가 힙에 삽입된 순서임
	- Infimum, supremum을 포함한 힙 레코드는 0번부터 번호가 매겨짐, Infimum은 항상 0, supremum은 항상 1임
	- 삽입된 사용자 레코드는 2부터 번호가 매겨짐
- Number of Records Owned
	- 페이지 디렉토리에서 현재 레코드가 '소유'한 레코드수
	- 향후 포스트에서 설명할 예정
- Info Flag
	- 레코드에 대한 boolean flag를 지정하는 4비트 비트맵
	- 현재 두개의 플래그만 정의도어 있음
		- min_rec(1)는 이 레코드가 B+Tree의 non-leaf에서 최소 레코드임을 의미함
		- deleted(2)는 레코드가 삭제 표시되어 있으며, 향후 purge operation에 의해 실제로 삭제될 것임을 의미함
- Nullable field bitmap(optional)
	- 필드가 NULL인지 여부를 저장하기 위한 필드, nullable한 필드당 1비트를 사용하고, byte로 반올림됨
	- 필드가 NULL인 경우 해당 필드 값은 레코드의 키 또는 행부분에서 제거됨
	- Null이 필드가 없는 경우 이 비트맵은 존재하지 않음
- Variable file lengths array(optional)
	- 가변길이 필드당 8비트 또는 16비트 정수 배열(필드의 최대크기에 따라 다름)로 해당 필드에 대한 데이터 길이를 저장
	- 가변길이 필드가 없는경우, 이 배열은 없음

- record header는 row당 최소 5 byte이며, 가변길이 필드에 의해 더 길어질 수 있음

### Clustered indexes
![center](Pasted%20image%2020240524153758.png#center)
- Cluster Key Fields
	- 클러스 키 필드는 문자 그대로 함께 연결됨
	- InnoDB는 column유형 별 내부 저장소 형식의 raw byte를 단이 바이트 스트림으로 연결하기만 함
- Transaction ID
	- 이 레코드를 마지막으로 수정한 트랜잭션의 48비트 정수 트랜직션 ID
- Roll Pointer
	- 해당 레코드를 마지막으로 수정한 트랜잭션의 undu record의 rollback segment 위치를 포함하고 있는 구조체
	- 이 필드의 roll pointer 구조는 1비트의 "삽입중" 플래그, 7비트의 rollback segment ID, 4바이트 페이지 번호, 2바이트의 undo log위치의 페이지 오프셋으로 이루어짐
- Non-Key Fields
	- 기본키가 아닌 실제 행데이터가 단일 바이트 스트림으로 연결되어 있음

![center](Pasted%20image%2020240524160646.png#c)

https://blog.jcole.us/2013/01/10/the-physical-structure-of-records-in-innodb/