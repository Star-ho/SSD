---
created: 2023-10-13T23:00:57
date: 2024-03-08T23:19
updated: 2024-03-31T22:43
---
- Disk에 데이터를 쓰기 전 데이터가 저장되는 메모리 영역
- 기본 크기는 16MB
- log buffer의 크기가 크다면, 큰 크기의 redo log를 써야하는 transaction에서 redo log를 disk에 옮기지않고 한번에 작업 가능
	- log buffer의 크기가 작으면 한 트랜잭션에서 redo log를 disk에 써야하는 작업을 중간에 실행해야 하기에 속도가 느려짐

#Database 
#Innodb 
#Log-Buffer
#Innodb-In-Memory-Structure 