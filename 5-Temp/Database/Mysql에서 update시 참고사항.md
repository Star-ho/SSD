---
date: 2023-11-17T22:24:21
updatedAt: 2024-04-21 18:34:36+0900
tags: 
---
- mysql 에서 update할때 where조건에 걸려있는 컬럼이 index가 아니라면, full table scan이 발생하고, 이로인해 전체 테이블의 락이 걸림



https://dba.stackexchange.com/questions/271197/does-update-lock-the-row-or-the-entire-table