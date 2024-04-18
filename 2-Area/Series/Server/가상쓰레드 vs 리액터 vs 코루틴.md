---
created: 2024-03-31T22:41:00
date: 2024-04-18T23:17
---
가상쓰레드, 리액터, 코루틴 이 세가지 프로젝트는 모두 Blocking I/O로 인한 병목을 줄이기 위해 사용하고있습니다.

기존에는 리액터, 코루틴으로 nonBlocking I/O를 사용했다면, 작년 가상쓰레드가 나온 이후, 과연 어떻게될 지에 대해 개인적인 의견 및 정보들을 작성하려 합니다.

우선 세가지 프로젝트의 목표에 대해 이야기 하려합니다.
## [리액터](https://www.reactive-streams.org/)
> The main goal of Reactive Streams is to govern the exchange of stream data across an asynchronous boundary—think passing elements on to another thread or thread-pool—while ensuring that the receiving side is not forced to buffer arbitrary amounts of data. In other words, back pressure is an integral part of this model in order to allow the queues which mediate between threads to be bounded. The benefits of asynchronous processing would be negated if the communication of back pressure were synchronous (see also the [Reactive Manifesto](http://reactivemanifesto.org/)), therefore care has to be taken to mandate fully non-blocking and asynchronous behavior of all aspects of a Reactive Streams implementation.

> 리액터는 리액티브 스트림즈의 구현체이기 떄문에 리액티
비동기 