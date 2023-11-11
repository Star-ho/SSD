 - atomicity, consistency, isolation, durability의 앞글자를 따온것
 - mysql의 트랜잭션과 밀접한 연관

### atomicity(원자성)
- 하나의 작업단위는 commit되거나 rollback 되어야 하는 성질
- 하나의 트랜잭션에서 여러 변경사항이 발생할 경우, 모두 성공되어 commit되거나, 모두 실패해서 rollback 되어야함

### concurrency(동시성)
- 트랜잭션은 트랜잭션이 진행되는 동안, 서로 격리됨

#wait-to-update 


https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_acid