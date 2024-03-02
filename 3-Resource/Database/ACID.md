---
date: 2023-11-11T23:25:12
---
 - atomicity, consistency, isolation, durability의 앞글자를 따온 것
 - mysql의 트랜잭션과 밀접한 연관관계를 가짐

### atomicity(원자성)
- 하나의 작업단위는 commit되거나 rollback 되어야 하는 성질
- 하나의 트랜잭션에서 여러 변경사항이 발생할 경우, 모두 성공되어 commit되거나, 모두 실패해서 rollback 되어야함
### consistency(일관성)
- transaction이 진행 중이거나, commit이나 rollback 후 모두 일관된 결과를 가져야함
- 여러 테이블에서 관련 데이터가 업데이트 될때, 모두 예전값을 보여주거나 새 값을 보여줘야함
- innodb에서는 첫 select가 발생한 시점으로 snap shot을 생성하여 트랜잭션 도중 같은 쿼리를 실행해도 같은 결과가 나옴
- 일관된 읽기 참조
### isolation(격리성)
- 트랜잭션은 트랜잭션이 진행되는 동안, 다른 트랜잭션에 영향을 주면 안됨
- lock을 통해 구현
### durability(내구성)
- 트랜잭션의 결과는 내구성을 가져야함
- commit동작이 성공적으로 끝나면, 전원공급, 시스템 오류등 어떤 장애가 나더라도 변경사항은 저장되어야함
- innodb는 double write buffer, redo 등 여러기능을 사용하여 내구성을 가짐

#Database
#ACID


https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_acid