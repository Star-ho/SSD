---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 17:28:32+9480
tags:
  - InnoDB-Architecture
  - "#Database"
  - "#hugo_blog"
categories: InnoDB
---
- 장애가 났을때, 종료되지 않았던 트랜잭션으로 부정확한 데이터의 정합성을 맞추기 위한 로그
- redo log는 SQL문이나 low level api call로 인한 변경요청을 인코딩해서 저장함
- 예기치못한 종료로 인해 변경이 발생하였지만 반영되지 않은 요청들을, 초기화 혹은 커넥션을 맺을때 redo로그를 replay하면서 데이터를 맞춤
- mysql의 데이터디렉토리 하위 \#InnoDB_redo에 위치


https://velog.io/@pk3669/Mysql-Redo-Undo-Log
https://dev.mysql.com/doc/refman/8.0/en/InnoDB-redo-log.html
#Database 
#InnoDB 