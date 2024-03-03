---
date: 2024-02-29T23:43:15
---
- 허가증을 유지함으로서 동시성을 제어
- acquire()메서드는 허가증이 사용가능할때까지 block하고 사용가능할때 허가증을 가짐
- release는 허가증을 추가하고, 잠재적으로 blocking되어있는 acquirer를 해제함

- 실제로 퍼미션 객체는 사용되지 않으며, 세마포어는 사용가능한 갯수를 카운팅할 뿐임

- Semaphore는 자원에 대해 접근할수 있는 쓰레드의 수를 제한하는데 사용함


## vs ReentrantLock
- ReentrantLock은 1개의 자원에 대해 1개의 쓰레드만 접근이 가능함
- Semaphore는 1개의 자원에 대해 n개의 쓰레드 접근이 가능함


## VarHandle
## ExcutersService
- CountDownLatch
## CAS
## ConcurrentCollection