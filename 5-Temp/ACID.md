 - atomicity, consistency, isolation, durability의 앞글자를 따온것
 - mysql의 트랜잭션과 밀접한 연관

### atomicity(원자성)
- 하나의 작업단위는 commit되거나 rollback 되어야 하는 성질
- 하나의 트랜잭션에서 여러 변경사항이 발생할 경우, 모두 성공되어 commit되거나, 모두 실패해서 rollback 되어야함


### consistency(일관성)
- tarnsaction이 진행되거나, commit 후, rollback 후 모두 일관된 결과를 가져야함

- 일관된 읽기 참조


### isolation(격리성)
- 트랜잭션은 트랜잭션이 진행되는 동안, 서로 격리됨
- innodb에서는 첫 select가 발생한 시점으로 snap shot을 생성하여 트랜잭션 도중 같은 쿼리를 실행해도 같은 결과가 나옴

### durability(내구성)
- 트랜잭션의 결과는 내구성을 가져야함
- commit동작이 성공적으로 끝나면, 전원공급, 
- double write buffer

#wait-to-update 


https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_acid