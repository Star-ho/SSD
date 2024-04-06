---
created: 2024-03-27T23:21
date: 2024-03-28T10:19
updated: 2024-04-06T23:30
---
> hikari가 일본어로 빛이라는 의미
## ConcurrentBag
- hikary cp 에서 커넥션을 관리하는 주체
- borrow(빌려줌)메서드으로 커넥션을 반환
	- Compare and set 연산으로 커넥션을 사용상태로 변경
- requite(갚음)메스드로 커넥션을 반납
	- setState 메서드로 커넥션을 사용가능한상태로 변경
> 빌려줄때는 CAS연산으로 해당 커넥션이 사용가능한 상태인지 확인하지만, 갚을때는 따로 확인하지 않음

## 왜 Hikari CP를 많이 사용하는가?
- Spring에서 지원하는 기본  connection pool이다
- Spring에서는 성능과 동시성에서 HikariCP가 장점이 있다고 판단하여 사용함
- 사용이 불가능한 상황에서는 아래와 같은 순서로 Connection pool을를 사용함
	- HikaryCP > Tomcat pooling DataSource > Commons DBCP2 > Oracle UCP
>참고
>https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#data.sql.datasource.connection-pool


## 속성 정리
### connectionTimeout
- 연결 타임아웃
- 기본 30초
- 짧게 설정할경우, 설정한 시간보다 조회하는 시간이 길면, time out error 발생

https://github.com/brettwooldridge/HikariCP

#argent 