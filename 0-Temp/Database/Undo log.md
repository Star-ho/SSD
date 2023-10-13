- 하나의 트랜잭션에 들어있는 undo log 레코드의 집합임
- clustered index 레코드에 대한 트랜잭션을 취소하는 방법에 대한 정보가 포함되어있음
	- 롤백시 사용
- 다른 트랜잭션에서 일관된 read작업의 일부로 원본데이터를 확인해야 할때, 수정되지 않은 데이터는 undo log에서 확인할 수 있음
	- Dirty read해결
- undo log segment에 존재
- 아래 4가지 경우에 undo log가 생성됨
	- 사용자가 정의한 테이블의 insert문
	- 사용자가 정의한 테이블의 update, delete문
	- 사용자가 정의한 임시테이블의 insert
	- 사용자가 정의함 임시 테이블의 update, delete문
    

https://dev.mysql.com/doc/refman/8.0/en/innodb-undo-logs.html

#Database
#Undo-log
#Dirty-read