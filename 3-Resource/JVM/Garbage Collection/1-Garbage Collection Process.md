- 앞의 Garbage Collection Concept에서는 heap이 나누어져 저장되는 것을 이해함
- 여기서는 나누어져 저장되는 것들의 상호작용에 대해 알아봄

### 1. Object Allocation

![[Pasted image 20240222231607.png|center|600]]
- 모든 새 객체들은 Eden 영역에 할당됨
- 애플리케이션을 처음 시작한다면 두 survivor영역은 비어있음

### 2. Filling the Eden Space
![[Pasted image 20240222232133.png|center|600]]
- Eden 영역이 꽉 찬다면, minor GC가 실행됨

### 3. Copying Referenced Objects
![[Pasted image 20240222232238.png|center|600]]
- Referenced 객체는 S0 servivor 영역으로 이동됨
- Unreferenced 객체는 삭제됨

### 4. Object Aging
![[Pasted image 20240222232408.png|center|600]]
- 다음 miner GC때 3의 동작이 한번 더 발생됨
- Referenced 객체는 suvivor 영역으로 이동하고, Unreferenced 객체는 삭제됨
- 3과 다른점은 S0에 존재했던 객체들이 S1영역 으로 간다는 것
- S0에서 S1으로 이동한 객체는 이동하면서 



https://d2.naver.com/helloworld/1329
https://d2.naver.com/helloworld/0128759
https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
https://developers.redhat.com/articles/2021/08/20/stages-and-levels-java-garbage-collection#generational_garbage_collection
https://developers.redhat.com/articles/2021/09/09/how-jvm-uses-and-allocates-memory#how_to_check_the_thread_stack_size
