Process 는 독립된 메모리 영역인 '힙'을 할당받는다.

Thread 는 Process 하위에 종속되는 보다 작은 단위이고, 각 쓰레드는 독립된 메모리 영역인 스택(Stack) 을 갖는다. Thread 를 하나 생성하면, 하나의 스택 메모리가 생기는 것이다. 각 쓰레드는 다른 쓰레드에게 스택 메모리를 공유할 수 없다. 하지만 프로세스의 힙은 속한 모든 Thread 가 공유할 수 있다.
