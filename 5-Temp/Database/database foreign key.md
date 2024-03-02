---
date: 2024-01-25T23:27:34
---
읽어보기
- https://junghyungil.tistory.com/m/178
- https://dba.stackexchange.com/questions/168707/what-is-locking-order-of-mysql-on-query-with-join-statement
- https://learn.microsoft.com/ko-kr/sql/relational-databases/tables/primary-and-foreign-key-constraints?view=sql-server-ver16


foreignkey는 참조 무결성 도구일뿐 성능과는 영향없음

mysql foreign key, join lock
어떨때 foreign key 제약조건

데이터 변경할때 기본적으로 x락이 걸리는데  
외래키가 걸려잇으면 외래키 친구들에게도 s락이 걸리면서  
[https://stackoverflow.com/questions/83147/whats-wrong-with-foreign-keys](https://stackoverflow.com/questions/83147/whats-wrong-with-foreign-keys)|


#wait-to-update