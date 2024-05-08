---
date: 2024-05-08 22:34:01
updatedAt: 2024-05-08 23:20:09
tags:
  - hugo_blog
  - B-tree
categories:
  - DataStructure
---
- 다수의 엘리먼트가 있을때, 지역성을 가질 수 있는 자료구조
	- 한번읽고, 다음걸 읽을때 빠르게 찾아갈 수 있기 때문	

## 특징
- 모든 데이터는 leaf노드에 있음
- non-leaf노드에는 키만 존재
- root노드에서 모든 leaf노드까지는 같음
- 만약, 노드에서 n개의 자식을 가지고 있으면, 이  노드는 n-1개의 키를 가지고 있음
- 루트노드를 제외한 모든 노드는 절반이상 차있음
- 하위노드의 모든 값은, 해당 부모 노드의 양쪽 포인터 값 사이에 있는 키를 가짐
- 루트노드가 leaf노드가 아닌경우, 적어도 2개의 자식을 가지고 있음


## 예제
- 아래 예제는 branch factor가 5인 B-tree임
	- branching factor가 5이기에, 리프가 아닌 노드들은 5개의 addr값을 가지고 있음
![center|700](Pasted%20image%2020240508231341.png)

### 29라는 값을 찾는 경로
1. 먼저 루트노드에서 10과 50사이의 주소를 찾음
2. 1에서 얻은 주소를 따라가, 25와 37사이의 주소를 얻음
3. 2에서 얻은 주소를 따라가 28과 31사이의 주소를 얻고, 해당 주소에서 값을 찾음
## 삽입과정
위의 트리에서 13,14,24 데이터를 넣는 과정임

![center](Pasted%20image%2020240508232003.png)
https://www.cs.cornell.edu/courses/cs3110/2012sp/recitations/rec25-B-trees/rec25.html
https://www.linkedin.com/pulse/data-structures-powering-our-database-part-3-b-trees-saurav-prateek/