---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:44:52+7780
tags: 
---
- X-Lock이 걸린 객체에 대해 다른 트랜잭션에서 읽기, 쓰기 불가능
- X-Lock이 걸린 객체에 대해 다른 객체에서 S-Lock, X-Lock 걸수 없음

- 변경 또는 삭제를 위해 락을 걸떄 활용
- Mysql의 Repeatable-Read는 Constent Read 기술을 사용해여 X-Lock걸린 row를 읽도록 함으로써 효율을 높임
	- X-Lock이 걸리기 전의 값을 읽음

https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html