---
date: 2024-04-21T15:02:55
updatedAt: 2024-04-21T15:07
tags: 
---
- 특정 행을 읽기위해 거는 락
- 어떤 object에 S-lock이 걸려있다면 다른 트랜잭션에서 읽기는 가능하지만 변경은 불가능함
- S-lock이 걸려있는 object에 S-lock를 또 걸 수 있지만 X-lock은 걸 수 없음


https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html