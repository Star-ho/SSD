---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 17:46:37+1210
tags:
  - Trouble-Shooting
  - Database
  - hugo_blog
categories:
  - Database
---

- 커넥션 관련 쿼리
```
-- 현재 mysql server에서 동시에 지원가능한 connection 가능 개수
show variables like '%max_connections%';

-- 서버가 시작된 후로 동시에 연결된 최대 connection 개수
SHOW STATUS WHERE `variable_name` = 'Max_used_connections';  

-- 현저 서버에 연결된 connection 수
SHOW STATUS WHERE `variable_name` = 'Threads_connected';
```



#MySQL 