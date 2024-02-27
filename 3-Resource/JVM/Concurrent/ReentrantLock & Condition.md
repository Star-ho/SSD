# ReentrantLock
- Lock 인터페이스의 구현체
- 
- synchronized method, statements와 기본적인 동작과 의미가 동일하지만 확장된 기능을 가짐
- synchronized 키워드를 사용할때보다 더 유연하게 사용가능

## 생성자
- 생정자에서 fair변수의 값을 받음
- fair가 true라면 잠금을 가장 오래 기다린 쓰레드에 엑세스 권한부여
	- false라면 특정 엑세스 순서를 보장하지 않음
	- fair가 true인 경우가 전체처리량이 낮을 수 있지만, lock을 얻는 편차가 적고, lock starvartion이 덜 발생함
	- fair가 true라도 쓰레드 스케줄링이 공정하지 않을 수 있음
		- 


- Condition
## Semaphore
## VarHandle
## ExcutersService
- CountDownLatch
## CAS



https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html