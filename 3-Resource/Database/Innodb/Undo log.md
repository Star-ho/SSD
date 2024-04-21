---
date: 2024-03-31T22:41:00
updatedAt: 2024-04-21 18:32:05+2240
tags:
  - InnoDB-Architecture
  - "#Database"
  - "#hugo_blog"
categories: InnoDB
---
- 하나의 트랜잭션에 들어있는 undo log 레코드의 집합임
- clustered index 레코드에 대한 트랜잭션을 취소하는 방법에 대한 정보가 포함되어있음
	- 롤백시 사용
- 다른 트랜잭션에서 일관된 read작업의 일부로 원본데이터를 확인해야 할때, 수정되지 않은 데이터는 undo log에서 확인할 수 있음
	- Dirty read해결
- rollback segments에 포함된 undo log segment에 존재
	- rollback segments의 undo log는 insert와 update로 나누어짐
	- insert undo log는 트랜잭션 롤백에만 사용이 되므로 트랜잭션이 커밋되면 폐기됨
	- update undo log는 일관적 읽기에 사용됨
	- 이전 버전의 데이터베이스 row를 만드는데 update undo log가 요구되는 일관적 읽기스냅샷이 필요하지 않을떄 삭제 가능
		- 업데이트 트랜잭션이 끝나기전 생성된 트랜잭션들이 모두 끝나야 삭제 가능
		- 읽기 일관성을 유지하기 위해
	- [참고](https://dev.mysql.com/doc/refman/8.0/en/InnoDB-multi-versioning.html)
- 아래 4가지 경우에 undo log가 생성됨
	- 사용자가 정의한 테이블의 insert문
	- 사용자가 정의한 테이블의 update, delete문
	- 사용자가 정의한 임시테이블의 insert
	- 사용자가 정의함 임시 테이블의 update, delete문
    

https://dev.mysql.com/doc/refman/8.0/en/InnoDB-undo-logs.html

#InnoDB 