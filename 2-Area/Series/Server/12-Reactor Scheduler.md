---
created: 2024-04-13T22:11
date: 2024-04-13T22:34
---
## 서론
- Reactor에 대해 여러가지 공부해 보았는데, reactor Scheduler에 대한 글이 없어 소스코드를 보며 분석하려한다.

## Reactor Scheduler
작업이 실행될 쓰레드를 결정하는 클래스
java reactor에서는 제공하는 여러가지 스케줄러를 제공하는데 이중 ImmediateScheduler, BoundedElasticScheduler, ParallelScheduler에 대해 알아보려 한다
- 이 중에서 현재 제일 많이 사용하고 있는 BoundedElasticScheduler에 대해 알아볼것이다.

## Schedulers
먼저 필드에 대해 알아보자 

### DEFAULT_POOL_SIZE
- ParallelScheduler에 사용시 설정되는 
DEFAULT_BOUNDED_ELASTIC_SIZE
DEFAULT_BOUNDED_ELASTIC_ON_VIRTUAL_THREADS
DEFAULT_BOUNDED_ELASTIC_QUEUESIZE
reactor-java에서 subcribeOn, publishOn메서드로 스케줄러를 할당한다



subscribeOn, publishOn에는 Schedulers의 정적 메서드를 사용하여 스케줄러를 지정하는데, 우선 지정하는 메서드부터 알아보자
	- 