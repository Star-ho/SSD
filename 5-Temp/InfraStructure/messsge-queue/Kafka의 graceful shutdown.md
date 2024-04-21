---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:44:52+9380
tags: 
---
Kafka의 graceful shutdown에 대해 공부해보고 있는데 Consumer 설정에서 shutdownTimeout을 어떤값으로 설정하던지 반영되지 않는것 같고 spring.lifecycle.timeout-per-shutdown-phase 설정값 만큼 대기하다가 종료되는데 뭔가 놓치고 있는 부분이 있을까요?

shutdownTimeout 설정값이 사용되는 AbstractMessageListenerContainer클래스의 stop 메서드를 디버깅해보아도 isRunning()메서드가 false여서 대기하는 로직도 타지 않는 것 같습니다 ㅠㅠ