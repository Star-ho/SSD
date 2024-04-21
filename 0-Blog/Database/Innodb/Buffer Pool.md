---
date: 2024-04-21T15:02:55
updatedAt: 2024-04-21T15:07
tags: 
---
- 접근했었던 테이블과 인덱스를 캐시하는 메인 메모리
- 속도를 높이기 위해 빈번히 접근하는 데이터를 메모리에서 바로 접근하게함
- 전용서버에서는 80%정도의 데이터를 메모리에 올려서 사용함

- Buffer Pool은 LRU알고리즘을 기반으로 데이터를 관리함
- 새로운 데이터를 읽을때, 가장 옛날에 읽은 데이터를 방출하고, 새로운 데이터를 Mid point에 넣음
![center|400](real-resource-image/Pasted%20image%2020231115224606.png)
- Innodb의 LRU알고리즘은 다음과 같음
	- buffer pool의 3/8은 old sublist에 할당
	- mid point는 new sublit의 tail과 old sublit의 head가 만나는 곳의 경계
	- 데이터가 처음 읽혀질때는 mid point에 데이터를 삽입
		- 데이터가 처음 읽혀지는 것은 사용자의 요청 혹은 innodb에서 자동으로 실행되는 read-ahead로 인한 읽기임
	- old 영역에 있는 데이터가 읽혀지면 young영역으로 이동
		- 사용자의 읽기로 인한 읽기면 즉시 young영역으로 이동
		- innodb의 read-ahead로 인한 읽기면 youn영역으로 이동하지 않음
	- innodb에서 노화는 young영역에서 old영역으로 이동하다 결국 evicted되는 것임


- [`SHOW ENGINE INNODB STATUS`](https://dev.mysql.com/doc/refman/8.0/en/innodb-standard-monitor.html "15.17.3 InnoDB Standard Monitor and Lock Monitor Output"),명령어로 buffer pool의 상태를 확인할 수 있음


- buffer pool의 자세한 설정은 아래 링크를 추가로 읽어볼것
https://dev.mysql.com/doc/refman/8.0/en/innodb-buffer-pool.html


#Innodb-In-Memory-Structure 