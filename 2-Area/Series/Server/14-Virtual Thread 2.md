---
date: 2024-03-31T22:41:00
updatedAt: 2024-05-07 22:26:17
tags:
  - Server-History
  - hugo_blog
  - virtual-thread
categories: Server-History
---
## Scheduler 및 동작방식
- Virtual Thread는 continuation으로 동작함
- Lock support의 park메서드에서 Virtual Thread일때 yield메서드를 호출함
	- blocking이 필요한 코드에서 중단이 발생한다는 것을 알 수 있음
- unpark메서드에서 submitRunContinuation을 호출하여 작업큐에 해당 작업을 추가함
 - cpu 

- fork join 
- 스케줄링 원리
- 작업단위 continiation
https://techblog.woowahan.com/15398/
https://www.youtube.com/watch?v=BZMZIM-n4C0