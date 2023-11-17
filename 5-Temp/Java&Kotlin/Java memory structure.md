![[Pasted image 20231117225008.png]]

### Native Method Stack
- C stack이라는 범용적인 스택을 사용
	- 내가 ollydbg봤던 스택
- 현재 실행중인 메서드의 정보를 포함함
	- 지역변수, 파라미터, 리턴주소 등
- 해당 스레드가 허용된것보다 더 큰 Native Method Stack이 필요한경우, StackOverflowError
- 해당 스레드가 허용된만큼 Native Method Stack이 필요하지만, 메모리가 부족한 경우 OutOfMemoryError
### PC Register
- 각각의 쓰레드마다 하나씩 가지고 있음
- 현재 실행중인 코드의 주소를 저장하고있음
- 실행중인 메서드가 native메서드가 아닐경우, 가상머신 명령어의 주소를 가지고 있음

### Stack Area
- 


### Heap Area
### Method Area

https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html

https://www.scaler.com/topics/memory-management-in-java/

https://shinjekim.github.io/java/2020/01/06/%EC%9E%90%EB%B0%94%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0/
#wait-to-update 