---
date: 2024-03-31T22:41:00
updatedAt: 2024-05-07 22:49:27
tags:
  - Server-History
  - virtual-thread
categories:
  - Server-History
---
## Scheduler 및 동작방식
- Virtual Thread는 continuation으로 동작함
- Lock support의 park메서드에서 Virtual Thread일때 yield메서드를 호출함
	- blocking이 필요한 코드에서 중단이 발생한다는 것을 알 수 있음
- unpark메서드에서 submitRunContinuation을 호출하여 작업큐에 해당 작업을 추가함
 - cpu당 1개의 워커? 하나의 스케줄러?

- fork join pool
	- work stealing
- 스케줄링 원리
- 작업단위 continuation

- vt의 park내에 yield가 존재
- vt 워킹큐

- syncronized에서는 왜 pinning? reenterant lock에서는 왜 안pinning?
- 현재 thread local에 어떤 정보가 있을지?

entity manager는 thread local에 있을텐데 괜찮을지

https://velog.io/@eastperson/synchronized%EC%99%80-ReentrantLock-%EA%B7%B8%EB%A6%AC%EA%B3%A0-JDK-21-Virtual-Thread
https://medium.com/javarevisited/synchronized-vs-reentrantlock-how-to-choose-cfb5306080e7
https://www.alibabacloud.com/blog/lets-talk-about-several-of-the-jvm-level-locks-in-java_596090?source=post_page-----84e78b76767b--------------------------------

#argent
https://techblog.woowahan.com/15398/
https://www.youtube.com/watch?v=BZMZIM-n4C0