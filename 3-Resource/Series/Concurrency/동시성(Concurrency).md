## 개념
- 프로그램, 알고리즘, 또는 문제의 부분이나 단위 등이, 결과에 영향을 주지 않고 특정한 순서없이 실행되거나 부분적인 순서만을 가지고 실행될 수 있는 성질 [링크](https://en.wikipedia.org/wiki/Concurrency_(computer_science))

 >하나의 작업을 정말 빠르게 처리하면 되지 않을까?
 >	- 대부분의 서비스에서는 cpu bound보다는 io bound가 많은 일을 처리하기에 동시성이 중요

> 동시성은 한번에 많은일을 처리하는것,
> 병렬성은 한번에 많은 일을 하는것을 의미

## 왜 중요한가?
- 한번에 여러가지 일을 처리하니 한번에 많은일을 처리할 수 있음
	- 성능이 증대됨

## But, 문제
- **하나의 자원으로 여러 작업을 진행함에 따라 문제가 발생**
- 무결성
	- 하나의 자원을 가지고 하나이상의 작업이 수행될때 자원의 무결성의 문제
	- ex) 하나의 계좌를 2가지 이유로 업데이트 할때

> 다양한 문제가 있을 수 있지만, 무결성이 제일 키 포인트 같아서 무결성만 적음


## 해결책
1. 기본 개념
	- mutex
	- semaphore

2. JAVA에서 코드레벨  lock [참고자료](https://www.baeldung.com/java-mutex)
	- synchronized
	- lock
	- Semaphore
	- Guava’s  Monitor

3. 데이터베이스에서 lock, isolation level
	- Shared Lock
	- Exclusive Lock
	- row lock
	- Record Lock
	- Gap Lock
	- Next-key Lock
	- isolation level
	- auto increment lock
	- table lock
		- read lock
		- write lock

4. 레디스를 이용한 분산락
	- Distribution Lock

https://stackoverflow.com/questions/11600520/synchronized-vs-reentrantlock-on-performance

https://stackoverflow.com/questions/74967004/row-level-locks-vs-index-record-locks

https://jaeseongdev.github.io/development/2021/06/16/Lock%EC%9D%98-%EC%A2%85%EB%A5%98-(Shared-Lock,-Exclusive-Lock,-Record-Lock,-Gap-Lock,-Next-key-Lock)/

https://stackoverflow.com/questions/74967004/row-level-locks-vs-index-record-locks

https://www.letmecompile.com/mysql-innodb-lock-deadlock/

https://www.google.com/search?q=mysql+row+lock&rlz=1C5CHFA_enKR1027KR1027&oq=mysql+row+lock&gs_lcrp=EgZjaHJvbWUyCQgAEEUYORiABDIHCAEQABiABDIHCAIQABiABDIHCAMQABiABDIHCAQQABiABDIGCAUQABgeMgYIBhAAGB4yBggHEEUYPNIBCDQ2MTJqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8

https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_intention_lock

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_lock

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_lock_mode

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_locking

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_transaction

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_acid

https://www.google.com/search?q=transaction+isolation+level&rlz=1C5CHFA_enKR1027KR1027&oq=transaction+is&gs_lcrp=EgZjaHJvbWUqBwgAEAAYgAQyBwgAEAAYgAQyBwgBEAAYgAQyBggCEEUYOTIHCAMQABiABDIHCAQQABiABDIHCAUQABiABDIHCAYQABiABDIGCAcQRRg80gEINTk4MGowajeoAgCwAgA&sourceid=chrome&ie=UTF-8

https://incheol-jung.gitbook.io/docs/q-and-a/spring/feat.-tmi

https://velog.io/@soyeon207/DB-Lock-%EC%B4%9D%EC%A0%95%EB%A6%AC-1-InnoDB-%EC%9D%98-Lock

https://incheol-jung.gitbook.io/docs/q-and-a/spring/feat.-tmi

https://worthpreading.tistory.com/90

https://bard.google.com/u/1/chat/f94bcbc80d01dd82?utm_source=sem&utm_medium=paid-media&utm_campaign=q3koKR_sem7

https://dev.mysql.com/doc/refman/8.0/en/innodb-information-schema.html

https://dev.mysql.com/doc/refman/8.0/en/innodb-information-schema-transactions.html

https://dev.mysql.com/doc/refman/8.0/en/innodb-information-schema-buffer-pool-tables.html

https://www.google.com/search?q=%EB%8F%99%EC%8B%9C%EC%84%B1+%EB%AC%B8%EC%A0%9C&rlz=1C5CHFA_enKR1027KR1027&oq=%EB%8F%99%EC%8B%9C%EC%84%B1+%EB%AC%B8%EC%A0%9C&gs_lcrp=EgZjaHJvbWUyCQgAEEUYORiABDIHCAEQABiABDIICAIQABgFGB4yCAgDEAAYBRgeMggIBBAAGAUYHjIICAUQABgFGB4yCAgGEAAYBRgeMggIBxAAGAUYHjIICAgQABgFGB4yCAgJEAAYBRge0gEIMjA3M2owajeoAgCwAgA&sourceid=chrome&ie=UTF-8

#wait-to-update 