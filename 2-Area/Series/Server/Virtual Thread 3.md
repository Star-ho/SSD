---
date: 2024-05-25 16:39:39
updatedAt: 2024-05-25 17:06:49
---
## Thread가 block되면 바로 context switching이 발생하는지
## Reactor에서 스택이 끊기는 이유


# spring에서 요청처리시 VirtualTread 생성하는 곳
AbstractEndpoint클래스에서 요청에 스레드를 할당함
AbstractEndpoint::processSocket이 요청을 처리하는 부분
NioEndpoint가 해당 클래스 구체 클래스


NioEndpoint.Poller::run
-> NioEndpoint::processKey
-> AbstractEndpoint::processSocket
-> Executer.execute(SocketProcessorBase)
	- vt설정시 이 Excuter가 바뀐다



http-nio prefix는 tomcat에서 붙임
	tomcat의 Http11NioProtocol

--- 

## VirtualThread의 scheduler 기본 생성 옵션

> 설명 앞선 설정이 없으면 뒤에걸로 설정됨
> VirtualThread::createDefaultScheduler
### parallelism 
1. system property에 `jdk.virtualThreadScheduler.parallelism`로 설정된값
2. Runtime.getRuntime().availableProcessors()로 얻은 프로세서 갯수
	- jvm옵션으로 실제 프로세서와 다르게 설정가능

### maxPoolSize
1. system property에  `jdk.virtualThreadScheduler.maxPoolSize`와 parallelism과 비교해서 작은값
2. 256과 parallelism과 비교해서 작은값

### minRunnable

- system property에 `jdk.virtualThreadScheduler.minRunnable`

---


## 기타 잡설들
### openjdk-21
Forkjoinpool-1-worker
ForkJoinPool.class에서 생성시 이름이 들어감


### spring boot
Threading.class에서 virtual쓰레드 사용여부 확인
- spring.threads.virtual.enabled 옵션

EmbeddedWebServerFactoryCustomizerAutoConfiguration.class에서 어떤 WebserverFactory사용할건지 결정

TomcatVirtualThreadsWebServerFactoryCustomizer.class에서 VirtualThreadExecutor설정
