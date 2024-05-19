---
date: 2024-05-19 22:44:51
updatedAt: 2024-05-19 23:23:59
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
- FSEG header
	- 이전 글에서 보았던, index root page의 FSEG헤더에는 포함됨
		- 해당 인덱스에서 사용하는 파일 세그먼트에 대한 포인터가 포함되어 있음
	- 다른 index page는 FSEG header를 사용되지 않고 0으로 채워짐
- INDEX header
	- Index 페이지 관리와 record관리에 필요한 필드가 포함되어 있음
	- 자세한 설명은 아래에 있음
- System records
	- 인덱스의 각 페이지에는 infimum과 supremum로 불리는 system record가 존재함
	- 이러한 레코드들은 페이지의 고정된 장소에 저장되어, 패이지 내에서 바로 접근이 가능함
- User records
	- 실제 데이터임
	- 각 레코드는 가변길이의 헤더와, 실제 데이터 컬럼을 가지고 있음
	- 헤더에는 오름차순으로 정렬된 singly-linked list를 구현하기 위한 next record 포인터를 포함함
	- 자세한 설명은 아래에 있음
- The page directory
	- FIL 트레일러에서 시작하여 페이지의 top에서 아래쪽으로 커지며(메모리 스택과 유사한 구조라고 생각됨), 페이지의 일부 레코드(4~8번째 레코드마다)에 대한 포인터를 포함함

## INDEX Header
![center](Pasted%20image%2020240519231114.png)
- Index ID
	- 해당 페이지가 속해있는 index의 ID를 의미함
- Format Flag
	- 해당 페이지 안에있는 record들의 포맷을 의미함
		- Number of Heap Record필드의 상위비트(0x8000)비트에 저장됨
	- 현재 COMPACT와 REDUNDANT가 가능함
		- 뒤에 자세히 설명함
- Number of Heap Records
	- infimum과 supremum 시스템 레코드, 삭제된garbage records를 포함한 페이지 내의 총 레코드 수를 의미함
- Heap Top Position
	- 현재 사용된 공간의 마지막 바이트 오프셋을 가르킴
	- heap 상단과 page directory의 마지막의 모든 공간은 여유공간임
- Garbage Space
	- garbage 레코드 콕록아네 있는 삭제된 레코드가 소비한 총 바이트 수를 저장함
- Last Insert Position
	- 페이지 내의 마지막으로 추가된 레코드의 바이트 오프셋을 저장함
- Page Direction
	- 현재 LEFT, RIGHT, NO_DIRECTION 세가지 값이 사용됨
	- 페이지가 순차적으로 insert되는지, 무작위로 insert되는지를 나타냄
	- 각 insert시 마지막 insert위치의 레코드를 일고, 해당 키를 insert된 레코드 키와 비교하여 insert방향을 결정함
- Number of 
