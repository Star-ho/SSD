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
	- ex) 하나의 계좌에 동시에 2번의 출금이 발생할떄
- 데드락, 효율성.. 등

> 다양한 문제가 있을 수 있지만, 무결성이 제일 키 포인트로 생각됨


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