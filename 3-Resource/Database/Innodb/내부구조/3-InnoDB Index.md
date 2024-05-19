---
date: 2024-05-19 22:44:51
updatedAt: 2024-05-19 22:45:05
---
## Index
- 물리적인 인덱스 구조를 알기전, InnoDB에서 Index에 대해 중요하게 알아야하는 아래 3가지에 대해 알아야 함
1. 모든 테이블은 primary key를 가지고 있다
	- 테이블 생성시 primary key를 설정하지 않는다면, 먼저 non-NULL unique키를 사용하고, 없다면 48bit의 숨겨진  ROW id를 primary key로 사용함
2. row data(primary key가 아닌 필드)는 primary key 인덳 구조 내에 저장됨
	- 이를 clustered key라고 명함
	- 인덱스 구조는 primary key필드에 키가 저장되며 row data는 해당 키에 연결된 값임(MVCC의 경우 추가적인 필드가 포함됨).
3. Secondary key는 동일한 인덱스 구조에 저장되며, 키는 해당한는 Secondary key이며, 값은 primary임

## Index page 구조

![center](Pasted%20image%2020240519225801.png)

- FIL header and trailer
	- 모든 페이지 유형에 일반적이고 공통적임
	- 다른 페이지 유형들과 다른점은, previous page와 next page 포인터가 인덱스 키를 기준으로 동일한 수준의 이전페이지와 다음페이지를 오름차순으로 가르킴
	- 이로인해 모든 페이지가 이중으로 연결된 double-linked list가 형성됨
- FSEG Header
	- 이전 글에서 보았던, index root page의 FSEG헤더에는 포함됨
		- 해당 인덱스에서 사용하는 파일 세그먼트에 대한 포인터가 포함되어 있음
	- 다른 index page는 FSEG Header를 사용되지 않고 0으로 채워짐
- 

