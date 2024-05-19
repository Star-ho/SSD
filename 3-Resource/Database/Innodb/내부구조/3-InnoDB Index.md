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
3. Secondary키는 동일한 인덱스 구조에 저장되며, 키는 해당 인덱스 