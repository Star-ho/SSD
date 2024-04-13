---
created: 2024-04-13T22:11
date: 2024-04-13T22:44
---
## 서론
- Reactor에 대해 여러가지 공부해 보았는데, reactor Scheduler에 대한 글이 없어 소스코드를 보며 분석하려한다.

## Reactor Scheduler
작업이 실행될 쓰레드를 결정하는 클래스
java reactor에서는 제공하는 여러가지 스케줄러를 제공하는데 이중 ImmediateScheduler, BoundedElasticScheduler, ParallelScheduler에 대해 알아보려 한다
- 이 중에서 현재 제일 많이 사용하고 있는 BoundedElasticScheduler에 대해 알아볼것이다.

## Schedulers
subscribeOn, publishOn에는 Schedulers의 정적 메서드를 사용하여 스케줄러를 지정하는데, 
reactor-java에서 subcribeOn, publishOn메서드로 스케줄러를 할당한다
스케줄러 할당은 S
먼저 필드에 대한 설명이다
### DEFAULT_POOL_SIZE
- 기본 풀 사이즈로, ParallelScheduler 사용 시쓰레드 갯수를 지정하는 필드이다.
- ```reactor.schedulers.defaultPoolSize``` 설정으로 값을 지정할 수 있으며 디폴트 값은 시스템의 CPU갯수이다

### DEFAULT_BOUNDED_ELASTIC_SIZE
- BoundedElasticScheduler에서 사용하는 쓰레드 풀 사이즈를 지정하는 필드이다.
- `reactor.schedulers.defaultBoundedElasticSize`로 설정할 수 있으며 디폴트는 시스템의 CPU갯수 \* 10개이다

### DEFAULT_BOUNDED_ELASTIC_QUEUESIZE
- BoundedElasticScheduler에서 쓰레드 별 큐사이즈를 지정하는 필드이다
- `reactor.schedulers.defaultBoundedElasticQueueSize`로 설정할 수 있으며 디폴트는 100,000개이다

### DEFAULT_BOUNDED_ELASTIC_ON_VIRTUAL_THREADS
- BoundedElasticScheduler사용 시 가상쓰레드 여부를 결정하는 필드이다
- reactor.schedulers.defaultBoundedElasticOnVirtualThreads로 설정할 수있으며, 디폴트로 false이다

이제 메서드에 대한 설명이다
- 메서드는






우선 지정하는 메서드부터 알아보자
	- 