- 여러 트랜잭션이 동시에 변경을 수행하고 쿼리를 수행할 때 성능과 안정성, 일관성 및 결과 재현성 간의 균형을 미세 조정하는 설정

## Read Uncommitted
- 가장 낮은 격리 수준
- 커밋되지 않은 다른 트랜잭션의 변경 내용을 읽을 수 있음
- 어떤 트랜잭션의 변경 내용이 COMMIT이나 ROLLBACK과 상관없이 다른 트랜잭션에서 보여짐
- Dirty Read(더티 리드)와 Non-Repeatable Read(반복 불가능한 읽기) 문제가 발생가능

## Read Committed
- 트랜잭션이 커밋된 데이터만 다른 트랜잭션에서 읽을 수 있음
- 다른 트랜잭션이 변경한 데이터는 읽을 수 없음
- Non-Repeatable Read 문제는 해결되지만, Phantom Read(유령 읽기) 문제는 발생함


## REPEATABLE READ
- 한 트랜잭션 내에서 같은 쿼리를 여러 번 실행했을 때, 항상 동일한 결과를 얻을 수 있음
- 첫번째 읽기 작업이 이루어진 때를 기준으로 스냅샷을 생성함

- Innodb의 default isolation level은 repeatable read

## Serializable