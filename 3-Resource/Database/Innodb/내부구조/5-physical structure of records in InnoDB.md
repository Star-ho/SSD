---
date: 2024-05-22 22:43:24
updatedAt: 2024-05-24 15:20:04
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


https://blog.jcole.us/2013/01/10/the-physical-structure-of-records-in-innodb/