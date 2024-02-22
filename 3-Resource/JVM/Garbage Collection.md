- 메모리 관리 기법중 하나로 프로그램이 동적으로 할당했던 메모리 영역 중에서 필요없게된 영역을 해제하는 기능

## Garbage Collection 과정

### Step 1. Marking
- Garbage Collector가 메모리 조각중에서 사용되고 있는 것과 사용되지 않는것을 찾아 marking하는 단계
![[Pasted image 20240222132054.png|center|400]]
- 그림에서 참조된 객체는 blue, 참조되지 않은 객체는 주황색임
- marking단계에서는 삭제를 하기 위한 객체를 찾는 과정
- 시스템을 모두 스캔해야 하는 경우 시간이 많이 소요될 수 있음
### Step 2. Normal Deletion
- Step 1에서 찾은 객체를 삭제하는 단계
![[Pasted image 20240222132435.png|center|400]]
- memory allocator는 새 객체를 할당 할 수 있는 여유 공간 블록에 대한 참조를 보유
	- memory allocator는 비어있는 공간에 대한 참조를 가지고, 할당이 필요한 비어있는 공간을 검색

### Step 2a. Deletion with Compacting
- 추가적인 성능 향상을 위해, 참조되지 않는 객체를 삭제하면서 남아있는 참조 객체를 압축할 수 있음
- 참조된 각체를 함께 이동함으로써, 메모리 할당은 더 빠르고 쉬워짐
![[Pasted image 20240222133340.png|center|400]]
- Memory Allocator는 비어있는 공간에 대한 첫번째 참조를 가지고, 메모리를 순차적으로 할당


https://d2.naver.com/helloworld/1329
https://d2.naver.com/helloworld/0128759
https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
https://developers.redhat.com/articles/2021/08/20/stages-and-levels-java-garbage-collection#generational_garbage_collection
https://developers.redhat.com/articles/2021/09/09/how-jvm-uses-and-allocates-memory#how_to_check_the_thread_stack_size

#ComputerScience
#java
#jvm