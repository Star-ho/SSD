# 사용하는 이유
### 쓰레드 동기화
- 멀티 쓰레드 환경에서 서로 다른 스레드가 하나의 자원을 공유해서 사용할때, 자원을 동시에 사용하면 예상치 않은 동작이 발생
	- ex) 두개의 쓰레드가 하나의 변수에 10을 증가시키려할때, 20이 증가되지 않고 10이 증가되는 문제
- 위와 같은 방법을 해결하기 위해 쓰레드를 동기화 하여 하나의 자원을 동시에 사용하지 못하는 방법

# 종류 및 사용방법

## Synchronized
## ReentrantLock
- Condition
## Volatile
## VarHandle
## ExcutersService
## CAS


https://www.ibm.com/docs/en/i/7.3?topic=techniques-synchronization-among-threads
https://www.linkedin.com/pulse/thread-synchronization-techniques-ensuring-order-concurrent-n/
https://www.linkedin.com/pulse/thread-synchronization-techniques-ensuring-order-concurrent-n/