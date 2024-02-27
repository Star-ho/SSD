# ReentrantLock
- Lock 인터페이스의 구현체
- 
- synchronized method, statements와 기본적인 동작과 의미가 동일하지만 확장된 기능을 가짐
- synchronized 키워드를 사용할때보다 더 유연하게 사용가능

## Fair
- 생정자에서 fair변수의 값을 받음
- fair가 true라면 잠금을 가장 오래 기다린 쓰레드에 엑세스 권한부여
- false라면 특정 엑세스 순서를 보장하지 않음
- fair가 true인 경우가 전체처리량이 낮을 수 있지만, lock을 얻는 편차가 적고, lock starvartion이 덜 발생함
- fair가 true라도 쓰레드 스케줄링이 공정하지 않을 수 있음
	- 쓰레드 A,B,C가 lock을 대기하고 순서도 A,B,C순일때, A가 lock을 점유하고 해제한뒤 A가 다시 lock 요청시 B와 C가 사용한 가 아닌, A가 다시 사용하는 현상
- tryLock 메소드는 fair필드의 여부와는 상관없음
- tryLock을 사용한다면, 다른 쓰레드가 대기중이더라도 lock을 점유할 수 있음

## Method
### lock()
- lock을 점유함
- 다른 스레드에서 lock을 점유하고 있지 않다면 lock을 점유하고 즉시 return함
- 현재 스레드에서 점유하고 있었다면, hold count를 1 증가시키고 즉시 return함
- 다른 스레드에서 점유중이라면 현재 스레드는 사용불가능하고 lock을 얻을 수 있을때 까지 대기함
	- lock을 얻는다면 hold count를 1로 세팅함
### unLock()
- lock을 헤제함
- 현재 스레드가 lock을 점유하고 있다면 hold count를 1 감소시킴
	- hold count가 0이 된다면 락을 해제함
- 현재 스레드가 lock을 점유하고 있지 않다면 illegalMonitorStateException 예외를 발생시킴

### tryLock


- Condition
## Semaphore
## VarHandle
## ExcutersService
- CountDownLatch
## CAS



https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html