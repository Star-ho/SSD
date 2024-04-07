---
created: 2024-04-07T12:24
updated: 2024-04-07T12:35
---
## 상황
- 현재 개발중인 기능에서 특정 api가 아래의 로그를 뱉으며 동작하지 않는 문제가 있다고 수정해달라는 요청을 받았다
```
Could not open JPA EntityManager for transaction; nested exception is org.hibernate.exception.JDBCConnectionException: Unable to acquire JDBC Connection
```

- 