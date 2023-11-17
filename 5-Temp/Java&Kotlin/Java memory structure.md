![[Pasted image 20231117225008.png]]
### PC Register
- 각각의 쓰레드마다 하나씩 가지고 있음
- 현재 실행중인 코드의 주소를 저장하고있음
- 실행중인 메서드가 native메서드가 아닐경우, 가상머신 명령어의 주소를 가지고 있음
### Java Virtual Machine Stacks
- C stack이라는 범용적인 스택을 사용
	- 내가 ollydbg봤던 스택
- 현재 실행중인 메서드의 정보를 포함함
	- 지역변수, 파라미터, 리턴주소 등
- 각각의 쓰레드가 하나씩 가지고 있음
- 해당 스레드가 허용된것보다 더 큰 Native Method Stack이 필요한경우, StackOverflowError
- 해당 스레드가 허용된만큼 Native Method Stack이 필요하지만, 메모리가 부족한 경우 OutOfMemoryError
### Native Method Stack
- JVM 스택과 유사하지만, java가 아닌 다른 언어로 작성된 네이티브 메서드를 지원하기 위한 영역
- C stack가지고, jvm stack과 같은 정보를 포함하고 있음
- jvm stack과 같은 상황에서 StackOverflowError, OutOfMemoryError가 발생함
### Heap Area
- 가상머신 쓰레드간 공유되는 메모리 영역
- 클래스의 인스턴스와 배열의 메모리가 할당되는 영역
- 가상머신이 시작될때 생성됨
- gc에 의해 회수되고, 명시적으로 회수할 수 없음
- 초기 메모리를 할당받고, 메모리가 더 필요하면 시스템에 요청해 메모리를 더 받아옴
- 
- 할당된 메모리보다 많은 메모리를 사용해야 할때 OutOfMemoryError발생
### Method Area

https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html

https://www.scaler.com/topics/memory-management-in-java/

https://shinjekim.github.io/java/2020/01/06/%EC%9E%90%EB%B0%94%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0/
#wait-to-update 