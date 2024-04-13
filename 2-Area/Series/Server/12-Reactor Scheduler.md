---
created: 2024-04-13T22:11
date: 2024-04-13T22:23
---
## Reactor Scheduler
- 작업이 실행될 쓰레드르 결정함
- java reactor에서 제공하는 스케줄러는 다음 4개임
	- ImmediateScheduler, BoundedElasticScheduler, ParallelScheduler, DelicateServiceScheduler
	- 이 중에서 ImmediateScheduler, BoundedElasticScheduler, ParallelScheduler에 대해 알아보자

- 