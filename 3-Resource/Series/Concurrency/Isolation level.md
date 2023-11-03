- 한글로 격리 수준
- 여러 트랜잭션이 동시에 변경을 수행하고 쿼리를 수행할 때 성능과 안정성, 일관성 및 결과 재현성 간의 균형을 미세 조정하는 설정입니다

- REPEATABLE READ
- 
- 첫번째 읽기 작업이 이루어진 때를 기준으로 스냅샷을 생성함

- Innodb의 default isolation level은 repeatable read
- 