---
date: 2023-11-13T22:36:38
updatedAt: 2024-04-24 23:36:48+5050
tags:
  - InnoDB-Architecture
  - "#Database"
  - "#hugo_blog"
categories: InnoDB
---
- 디스크의 데이터 파일이나 인덱스 정보를 메모리에 캐시해 두는 공간
	- 데이터 블록을 저장
- 속도를 높이기 위해 빈번히 접근하는 데이터를 메모리에서 바로 접근하게함
- 전용서버에서는 80%정도의 데이터를 메모리에 올려서 사용함

- 쓰기 작업을 지연시켜 일괄 작업으로 처리할수 있는 버퍼역할도 제공

- InnoDB 엔진은 페이지 크기 조각을 관리하기위해 LRU리스트, 플러시 리스트, 프리 리스트 3개의 자료구조로 버퍼풀을 관리

- 프리 리스트는 실제 사용자 데이터로 채워지지않은 비어있는 페이지의 목록

- 플러시 리스트는 동기화되지 않은 데이터를 가진 데이터페이지(더티페이지)의 변경 시점 기준의 페이지 목록을 관리
	- 

- Buffer Pool은 LRU알고리즘을 기반으로 데이터를 관리함
- 새로운 데이터를 읽을때, 가장 옛날에 읽은 데이터를 방출하고, 새로운 데이터를 Mid point에 넣음
![center|400](real-resource-image/Pasted%20image%2020231115224606.png)
- InnoDB의 LRU알고리즘은 다음과 같음
	- buffer pool의 3/8은 old sublist에 할당
	- mid point는 new sublit의 tail과 old sublit의 head가 만나는 곳의 경계
	- 데이터가 처음 읽혀질때는 mid point에 데이터를 삽입
		- 데이터가 처음 읽혀지는 것은 사용자의 요청 혹은 InnoDB에서 자동으로 실행되는 read-ahead로 인한 읽기임
	- old 영역에 있는 데이터가 읽혀지면 young영역으로 이동
		- 사용자의 읽기로 인한 읽기면 즉시 young영역으로 이동
		- InnoDB의 read-ahead로 인한 읽기면 youn영역으로 이동하지 않음
	- InnoDB에서 노화는 young영역에서 old영역으로 이동하다 결국 evicted되는 것임


- [`SHOW ENGINE InnoDB STATUS`](https://dev.mysql.com/doc/refman/8.0/en/InnoDB-standard-monitor.html "15.17.3 InnoDB Standard Monitor and Lock Monitor Output"),명령어로 buffer pool의 상태를 확인할 수 있음


- buffer pool의 자세한 설정은 아래 링크를 추가로 읽어볼것
https://dev.mysql.com/doc/refman/8.0/en/InnoDB-buffer-pool.html
Real Mysql 8.0

#InnoDB-In-Memory-Structure 