---
created: 2024-04-07T12:24
updated: 2024-04-07T12:45
---
## 상황
- 현재 개발중인 기능에서 특정 api가 아래의 로그를 뱉으며 동작하지 않는 문제가 있다고 수정해달라는 요청을 받았다.
```
org.springframework.transaction.CannotCreateTransactionException: Could not open JPA EntityManager for transaction; nested exception is org.hibernate.exception.JDBCConnectionException: Unable to acquire JDBC Connection
<생략>
Caused by: java.sql.SQLTransientConnectionException: write-pool - Connection is not available, request timed out after 30000ms.
```
- write-pool에서 커넥션을 가져올 수 없다는 로그였다.
- 테스트 서버였고, 커넥션 10개로 설정되어있었다.
- 다른 업무도 있었고, 단순 커넥션 부족이라고 생각해서 테스트 서버를 재시작하였고, 커넥션 갯수를 20개 까지 늘렸다
> 큰 착오였다, 테스트 서버에서 작업하는 인원은 5명이 채 되지 않았고, 절대 커넥션이 모자라지 않는 개수인데 당시에는 다른 작업으로 바빳고 대수롭지 않게 생각했었다

- 그 이후 2일뒤 커넥션 갯수를 늘려도 계속 에러가 나서 수정요청을 받았다.
- 커넥션 수가 모자랄리가 없다고 판단했는데, 계속 에러가 난다고하여 우선 커넥션 관련 로그 설정을 하였다
```yml
logging:  
  level:  
    com.zaxxer.hikari.HikariConfig: DEBUG  
    com.zaxxer.hikari: TRACE  
    org.springframework.transaction.interceptor: TRACE  
```

- 위 로그를 설정하고, 서버 로그를 확인해보니, write-pool의 커넥션이 api요청이 끝난 후에도 반환되지 않는 것을 확인했다.
```
DEBUG 57394 --- [l-1 housekeeper] com.zaxxer.hikari.pool.HikariPool        : write-pool - Pool stats (total=20, active=0, idle=19, waiting=0)
DEBUG 57394 --- [l-1 housekeeper] com.zaxxer.hikari.pool.HikariPool        : write-pool - Pool stats (total=20, active=1, idle=18, waiting=0)
DEBUG 57394 --- [l-1 housekeeper] com.zaxxer.hikari.pool.HikariPool        : write-pool - Pool stats (total=20, active=2, idle=17, waiting=0)
```
- connection을 사용한 후  connection이 반환되지 않는 connection leak이 있는것을 확인하였고, hikariConnec