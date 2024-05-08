---
date: 2024-05-08 22:34:01
updatedAt: 2024-05-08 23:06:28
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


![center](Pasted%20image%2020240508225722.png)


https://www.cs.cornell.edu/courses/cs3110/2012sp/recitations/rec25-B-trees/rec25.html
https://www.linkedin.com/pulse/data-structures-powering-our-database-part-3-b-trees-saurav-prateek/