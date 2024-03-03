---
created: 2024-02-22T23:19
updated: 2024-03-03T23:16
---

## Serial GC
- CPU 코어가 1개일때 적절함
- major GC와 minor GC가 serially하게 적용됨
- mark-compact-swap 방식을 사용
- 오래된 메모리를 heap의 시작점에 두고, 새로 생성된 메모리를 heap의 마지막에 두어 새로 생성된 메모리가 연속적으로 할당되게함
- 