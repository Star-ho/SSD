- IS, IX lock과 S,X Lock과의 차이는 테이블까지 락이 걸림
- IS, IX lock을 걸면 해당 테이블에 SHARED_READ 메타데이터락이 걸림
- 해당 테이블에 대해 다른 트래잭션에서 같은 테이블의 다른 row에 IS,IX락은 걸 수 있지만, 같은 테이블에 대해 S,X Lock을 걸 수 없음(실험완료)
	- 읽기나 쓰기 도중 테이블이 변경되는것을 막기 위함이라고 추측함

[Intention shared lock](https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_intention_shared_lock "intention shared lock")

- 아래의 명령어로 IS lock을 걸 수 있음
	- select .. lock in share mode ;  
	- select ..  for share ;  
	- 현재(8.0 기준) for share가 lock in share mode를 대체 하려하나 하위호환성 보장을 위해 lock in share mode를 유지하는중
	- 그러나, for share를 사용하면 OF table_name, NOWAIT, and SKIP LOCKED를 사용할 수 있음
> SELECT ... FOR SHARE is a replacement for SELECT ... LOCK IN SHARE MODE, but LOCK IN SHARE MODE remains available for backward compatibility. The statements are equivalent. However, FOR SHARE supports OF table_name, NOWAIT, and SKIP LOCKED options. See Locking Read Concurrency with NOWAIT and SKIP LOCKED.


https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_shared_lock


[`SELECT ... FOR UPDATE`](https://dev.mysql.com/doc/refman/8.0/en/select.html "13.2.13 SELECT Statement")문으로 X-lock을 걸 수 있음