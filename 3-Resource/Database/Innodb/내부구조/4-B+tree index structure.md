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
	- tree는 균형이 잡혀있고, 모든 가지의 깊이는 동읾함