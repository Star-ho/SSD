# 사용하는 이유
### 쓰레드 동기화
- 멀티 쓰레드 환경에서 서로 다른 스레드가 하나의 자원을 공유해서 사용할때, 자원을 동시에 사용하면 예상치 않은 동작이 발생
	- ex) 두개의 쓰레드가 하나의 변수에 10을 증가시키려할때, 20이 증가되지 않고 10이 증가되는 문제
- 위와 같은 방법을 해결하기 위해 쓰레드를 동기화 하여 하나의 자원을 동시에 사용하지 못하는 방법

# 종류 및 사용방법

## Synchronized
- java에서는 synchronized method와 synchronized statment를 제공함
### synchronized method
```kotlin
class SynchronizedCounter {  
    private var c = 0  
  
    @Synchronized  
    fun increment() {  
        c++  
    }  
  
    @Synchronized  
    fun decrement() {  
        c--  
    }  
  
    @Synchronized  
    fun value(): Int {  
        return c  
    }  
}
```
- synchronized 메소드를 사용하면 아래 2가지 효과를 얻을 수 있음
	- 동일한 객체에 대해 synchronized 메서드 호출이 동시에 발생되지 않음
		- 한 스레드가 객체에 대해 synchronized 메서드를 실행하면, 첫번째 쓰레드가 작업을 완료할때까지 동기화된 메서드를 호출하는 다른 모든 쓰레드가 block됨
	- synchronized된 메서드가 종료되면, 동일한 객체에 대한 synchronized 메서드의 후속  호출과 함께 happends-before 관계가 설립됨
		- 이로인해 모든 스레드에서 해당 객체 상태가 변경된 것을 확인할 수 있음
- 생성자 메소드에는 synchronized를 호출할 수 없음
## ReentrantLock
- Condition
## Volatile
## VarHandle
## ExcutersService
- CountDownLatch
## CAS


https://www.ibm.com/docs/en/i/7.3?topic=techniques-synchronization-among-threads
https://www.linkedin.com/pulse/thread-synchronization-techniques-ensuring-order-concurrent-n/
https://www.linkedin.com/pulse/thread-synchronization-techniques-ensuring-order-concurrent-n/