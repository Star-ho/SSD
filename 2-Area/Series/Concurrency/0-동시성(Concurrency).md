## 개념
- 프로그램, 알고리즘, 또는 문제의 부분이나 단위 등이, 결과에 영향을 주지 않고 특정한 순서없이 실행되거나 부분적인 순서만을 가지고 실행될 수 있는 성질 [링크](https://en.wikipedia.org/wiki/Concurrency_(computer_science))

 >하나의 작업을 정말 빠르게 처리하면 되지 않을까?
 >	- 대부분의 서비스에서는 cpu bound보다는 io bound가 많은 일을 처리하기에 동시성이 중요

> 동시성은 한번에 많은일을 처리하는것,
> 병렬성은 한번에 많은 일을 하는것을 의미

## 왜 중요한가?
- 한번에 여러가지 일을 처리하니 한번에 많은일을 처리할 수 있음
	- 성능이 증대됨

## But, 무결성의 문제
- **하나의 자원을 가지고 하나이상의 작업이 수행될때 자원의 무결성의 문제**
- Lost Update Problem(write-write conflict)
	- 하나의 로우에 동시에 여러번 변경이 발생했을 때 발생하는 문제
![[Pasted image 20231218230909.png|center|400]]
- Unrepeatable Read Problem
	- 다른 트랜잭션에서 변경이 되어, 같은 조회 쿼리에서 다른 데이터가 오는 현상
![[Pasted image 20231218231144.png|center|400]]
- Temporary Update Problem( dirty read problem)
	- 커밋되지 않은 데이터를 읽어서 발생하는 문제
![[Pasted image 20231218231800.png|center|400]]
- Incorrect Summary Problem
	- 
- Phantom Read Problem
	- 데이터가 삭제되어 같은 트랜잭션에서 데이터를 못가져오는 문제
![[Pasted image 20231218231610.png|center|400]]


## 해결책
1. 개념
	- critical section
	- mutex
	- semaphore

3. JAVA에서 코드레벨  lock [참고자료](https://www.baeldung.com/java-mutex)
	- synchronized
	- lock
	- Semaphore
	- Guava’s  Monitor

4. 데이터베이스에서 동시성 문제 처리
	- lock mode
		- Shared Lock
		- Exclusive Lock
	- lock type
		- row lock
		- Record Lock
		- Gap Lock
		- Next-key Lock
		- auto increment lock
		- table lock
		- insert intention lock
	- isolation level

5. Named Lock
	- redis
	- database



#Concurrency 

https://medium.com/@bindubc/distributed-system-concurrency-problem-in-relational-database-59866069ca7c