---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:23:53+8210
---
- file descriptor는 OS에서 관리하는 자원 중 하나임
- file descriptor가 너무 많으면 메모리를 많이 잡아먹음
	- 일정 수준이 넘어가면 불필요하다고 판단하기에 일정수준을 넘는 fd요청은 에러를 발생킴
	- JVM에서는 soft limit을 기준
- 적정량이 많으면 too many open files에러를 받아옴
	- fd를 얻는것 또한 시스템 콜이기에 fd를 얻을때 error를 발생시킴