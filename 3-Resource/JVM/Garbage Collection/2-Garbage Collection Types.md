---
created: 2024-02-22T23:19
updated: 2024-03-04T13:35
---

## Serial GC
- CPU 코어나 메모리가 적을 때 유용
- 하나의 서버에 여러 jvm이 실행되는 환경에서 유용
- major GC와 minor GC가 serially하게 적용됨
- mark-compact-swap 방식을 사용
- 오래된 메모리를 heap의 시작점에 두고, 새로 생성된 메모리를 heap의 마지막에 두어 새로 생성된 메모리가 연속적으로 할당되게함
- -XX:+UseSerialGC 로 사용가능

## Parallel GC
- 사용하는 알고리즘은 Serial GC와 같으나, 여러 스레드를 사용함
- CPU코어가 1개 이상일때 많을때 유용함
- CPU코어가 N개일때 N개의 garbage Collector를 사용
	- 옵션으로 garbage Collector갯수 설정 가능
- CPU코어가 1개인 환경에서는 Parallel GC를 사용하더라도 해당 Serial GC가 사용됨

- ParallelGC는 2가지 가 있음
### ParallelGC

### ParallelOldGC



