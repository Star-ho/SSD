- 데이터베이스는 성능상의 이유로 매 변경마다 데이터를 디스크에 쓰는게 아닌 메모리에 기록함
- 이후 주기적으로 메모리에 있는 데이터를 디스크에 저장하는데, 성공적으로 디스크에 저장된 최신의 레코드가 체크포인트임
- 이 체크포인트는 성공적으로 저장된 것이므로 체크포인트 장애나 충돌로 인한 복구시 체크포인트 이후의 로그를 사용하여 복구하면 시간이 단축됨
- 레코드 뿐만 아니라 트랜잭션 정보도 저장함

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_checkpoint
https://learn.microsoft.com/en-us/sql/relational-databases/logs/database-checkpoints-sql-server?view=sql-server-ver16

#Database 
#CheckPoint