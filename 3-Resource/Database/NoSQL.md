---
date: 2024-04-27 22:38:10+0980
updatedAt: 2024-04-27 22:54:25+4960
---
## 정의
- 기존의 RDBMS에서 데이터는 테이블이라는 데이터베이스 객체에 저장됨
- NoSQL에서는 데이터가 테이블단위로 저장되는 것이 아닌, Json 객체의 컬렉션으로 저장됨

- SQL은 구조화된 질의문(Structured Query Language)임
	- 구조화 되었다는 것은 사전 정의된 스키마에 따라 데이터가 저장된다는 것
- NoSQL은 SQL과 다르게 스키마를 정의하지 않아도됨

- RDMS에서는 하나의 테이블이 다른 테이블과 연관관계를 가지고 있음
	- 데이터베이스 내부에서 JOIN으로 데이터를 가져올 수 있음
- NoSQL에서는 연관관계를 가지고 있지 않으며, 필요시 application에서 JOIN이 가능함

## 장점
- RDBMS에 비해 수평적 확장에 용이함
	- 데이터베이스 서버를 늘려서 증가되는 트래픽에 대응할 수 있음
	- 서버를 늘려서 부하 분산가능

## 단점
- 데이터가 정규화 되어 있지않아, 고도로 정규화되고 정확한 데이터가 필요한 금융, 회계시스템에는 맞지 않음

https://www.oracle.com/kr/database/nosql/what-is-nosql/
https://blogs.oracle.com/mysql/post/qa-with-the-mysql-community-team