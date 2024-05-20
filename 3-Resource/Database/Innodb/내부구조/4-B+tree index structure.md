---
date: 2024-05-20 23:10:14
updatedAt: 2024-05-20 23:10:50
---
## B+Tree, root, leaf, level 용어정리
- B+Tree는InnoDB 인덱스의 구조
- 데이터가 메모리 크기와 일치하지 않아, 디스크에서 읽어야하는 경우 효율적임
	- 트리의 깊이에 따라 요청된 데이터에 엑세스하는데 필요한 최대 읽기 횟수가 고정되어 있어 확장성이 뛰어남

- 인덱스 트리는 트리에 엑세스하기 위한 시작점으로 root 페이지에서 시작됨
	- root page는 InnoDB의 data dictionary에 영구적으로 저장되어 있음
	- 트리는 단일 루트 페이지일만큼 작을 수 있고, multi-level tree의 수백만 페이지 일 수 있음

- 페이지를 leaf(internal)과 non-leaf(node)페이지로 구분함
	- leaf 페이지에는 실제 행 데이터가 포함됨
	- non-leaf페이지는 다른 non-leaf페이지 또는 leaf 페이지를 가지고 있음
	- tree는 균형이 잡혀있고, 모든 가지의 깊이는 동일함

- InnoDB는 트리의 각 페이지에 level을 할당함
	- 리프페이지에는 level 0을 할당하고, 트리 위로 올라갈수록 level이 증가함
	- root page의 level은 트리의 깊이와 같음
	- 구분이 중요하지 않은 경우, leaf페이지와 non-leaf페이지는 둘다 internal페이지라고 부름

## Leaf and non-leaf page
- leaf와 non-leaf페이지(Infimum과 supreme을 포함)는 next record의 오프셋을 저장한 "next record"포인터를 가지고 있음
- 이 연결은 infimum에서 시작하여 모든 레코드를 오름차순으로 연결되며, sumpemum에서 끝남
- 레코드는 물리적으로 정렬되어 있지 않고, 링크된 목록에서의 위치가 유일한 순서임
	- insert시 사용 가능한 공간이 있으면 insert됨
![center](Pasted%20image%2020240520232314.png)
- leaf page의 구조로, 각 레코드의 데이터의 일부로 키가 아닌 값을 가지고 있음

![center](Pasted%20image%2020240520232449.png)
- non-leaf페이지는 동일한 구조를 가지지만, 데이터로 하위 페이지 번호를 가르키며, 정확한 키 대신 하위페이지의 가장 작은 키를 가짐

![center](Pasted%20image%2020240520232622.png)
- 대부분의 인덱스는 2개 이상의 페이지로 구성되며, 여러 페이지가 오름차순 및 내림차순으로 링크되어 있음
- 각각의 페이지는 