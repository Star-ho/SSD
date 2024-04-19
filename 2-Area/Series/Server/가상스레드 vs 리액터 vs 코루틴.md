---
created: 2024-03-31T22:41:00
date: 2024-04-19T09:26
---
가상쓰레드, 리액터, 코루틴 이 세가지 프로젝트는 모두 Blocking I/O로 인한 병목을 줄이기 위해 nonBlocking I/O를 사용할 목적으로 쓰이고 있습니다.

기존에는 리액터, 코루틴으로 nonBlocking I/O를 사용했다면, 작년 가상쓰레드가 나온 이후, 과연 어떻게될 지에 대해 개인적인 의견 및 정보들을 작성하려 합니다.

우선 세가지 프로젝트의 목표에 대해 이야기 하려합니다.
## [리액터](https://www.reactive-streams.org/)
> 리액터는 리액티브 스트림즈의 구현체이기 떄문에 리액티브 스트림즈의 목표를 가져왔습니다

`The main goal of Reactive Streams is to govern the exchange of stream data across an asynchronous boundary—think passing elements on to another thread or thread-pool—while ensuring that the receiving side is not forced to buffer arbitrary amounts of data. In other words, back pressure is an integral part of this model in order to allow the queues which mediate between threads to be bounded. The benefits of asynchronous processing would be negated if the communication of back pressure were synchronous (see also the [Reactive Manifesto](http://reactivemanifesto.org/)), therefore care has to be taken to mandate fully non-blocking and asynchronous behavior of all aspects of a Reactive Streams implementation.`

간단히 요약해보자면
`비동기 뿐만이 아닌, 쓰레드간 element들을 교환하며 백프레셔를 지원하여 수신측에서 리소스를 지원한다`
입니다

리액터는 비동기 뿐만이 아닌, 배압까지 신경쓰고 있는 것을 알 수 있습니다

## [코루틴](https://github.com/Kotlin/KEEP/blob/master/proposals/coroutines.md)

`No dependency on a particular implementation of Futures or other such rich library;
`Cover equally the "async/await" use case and "generator blocks";`
`Make it possible to utilize Kotlin coroutines as wrappers for different existing asynchronous APIs (such as Java NIO, different implementations of Futures, etc).`

코루틴의 목표는`Futures와 다른 라이브러리 의존 없이, 비동기 api의 래퍼를 제공`하는것 입니다

## [가상 스레드](https://openjdk.org/jeps/444)

`Enable server applications written in the simple thread-per-request style to scale with near-optimal hardware utilization.`
`Enable existing code that uses the java.lang.Thread API to adopt virtual threads with minimal change.`
`Enable easy troubleshooting, debugging, and profiling of virtual threads with existing JDK tools.`

가상스레드의 목표는 `최소한의 변경으로, 현재 서버 애플리케이션이 작성된 요청당 스레드 모델의 최적화된 하드웨어 사용`이라는 것을 알 수 있습니다.



