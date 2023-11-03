- 어떤 object에 S-lock이 걸려있다면 다른 트랜잭션에서 읽기는 가능하지만 변경은 불가능함
- S-lock이 걸려있는 object에 S-lock를 또 걸 수 있지만 X-lock은 걸 수 없음




- 아래의 명령어로 lock을 걸 수 있음
	- select .. lock in share mode ;  
	- select ..  for share ;  
	- 현재(8.0 기준) for share가 lock in share mode를 대체 하려하나 하위호환성 보장을 위해 lock in share mode를 유지하는중
	- 그러나, for share를 사용하면 OF table_name, NOWAIT, and SKIP LOCKED를 사용할 수 있음
> SELECT ... FOR SHARE is a replacement for SELECT ... LOCK IN SHARE MODE, but LOCK IN SHARE MODE remains available for backward compatibility. The statements are equivalent. However, FOR SHARE supports OF table_name, NOWAIT, and SKIP LOCKED options. See Locking Read Concurrency with NOWAIT and SKIP LOCKED.


https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_shared_lock