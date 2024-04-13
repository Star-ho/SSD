---
created: 2024-04-13T22:11:25
date: 2024-04-13T23:14
---
## 서론
- Reactor에 대해 여러가지 공부해 보았는데, reactor Scheduler에 대한 글이 없어 소스코드를 보며 분석하려한다.

## Reactor Scheduler
실제 작업이 실행될 쓰레드를 할당하는 클래스이다.
java reactor에서는 제공하는 여러가지 스케줄러를 제공하는데, 이 중 reactor-netty에서 디폴트로 제공하는  BoundedElasticScheduler에 대해 집중적으로 알아볼 것이다

## Schedulers
subscribeOn, publishOn에는 Schedulers의 정적 메서드를 사용하여 스케줄러를 지정하기에 Schedulers클래스 부터 알아보자

필드에 대한 설명이다
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

이제 스케줄러를 생성하는 메서드에 대해 알아보자
```java
public static Scheduler boundedElastic() {  
    return cache(CACHED_BOUNDED_ELASTIC, BOUNDED_ELASTIC, BOUNDED_ELASTIC_SUPPLIER);  
}
```
스케줄러를 생성하는 메서드는 static메서드이고 내부에서 cache로 관리한다.
- 한번 스케줄러를 생성하면 내부에서 캐싱된 스케줄러를 가져온다는것을 알 수있다.
- ImmediateScheduler, BoundedElasticScheduler, ParallelScheduler는 다 아래와 같은 형태이다
> prefix로 new가 붙은 메서드를 사용하거나 fromExecuter를 사용해서 새로운 스케줄러를 생성할 수 있다.

```java
static CachedScheduler cache(AtomicReference<CachedScheduler> reference, String key, Supplier<Scheduler> supplier) {  
    CachedScheduler s = reference.get();  
    if (s != null) {  
       return s;  
    }  
    s = new CachedScheduler(key, supplier.get());  
    if (reference.compareAndSet(null, s)) {  
       return s;  
    }  
    //the reference was updated in the meantime with a cached scheduler  
    //fallback to it and dispose the extraneous one    s._dispose();  
    return reference.get();  
}
```
cache메서드 간단하다. 
캐싱된 스케줄러가 있는지 확인하고, 있으면 캐싱된 스케줄러를 반환하고, 없다면 인자로 받은 Scheduler Supplier로 스케줄러를 생성하고, 이를 캐싱한다.

그럼 이제 BoundedElasticScheduler를 생성하는 BoundedElasticSchedulerSupplier에 대해 알아보자
```java
class BoundedElasticSchedulerSupplier implements Supplier<Scheduler> {

	static final Logger logger = Loggers.getLogger(BoundedElasticSchedulerSupplier.class);

	@Override
	public Scheduler get() {
		if (DEFAULT_BOUNDED_ELASTIC_ON_VIRTUAL_THREADS) {
			logger.warn(
					"Virtual Threads support is not available on the given JVM. Falling back to default BoundedElastic setup");
		}

		return newBoundedElastic(DEFAULT_BOUNDED_ELASTIC_SIZE,
				DEFAULT_BOUNDED_ELASTIC_QUEUESIZE,
				BOUNDED_ELASTIC,
				BoundedElasticScheduler.DEFAULT_TTL_SECONDS,
				true);
	}
}
```
newBoundedElastic메서드에 Schedulers의 BoundedElasticScheduler의 설정값이 들어가는 것을 볼 수 있다.

