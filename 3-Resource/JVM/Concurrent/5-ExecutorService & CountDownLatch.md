---
created: 2024-03-03T17:25
updated: 2024-03-03T17:46
---
# ExecutorService
- 비동기 작업을 할때 쓰레드관리가 복잡한 과정임
	- ExecutorService가 복잡한 쓰레드관리를 단순화 시켜줌
- 하나이상의 비동기 작업을 과정을 추적하기 위한 Future를 생성하는 메서드와 종료관리 메서드를 제공
- Excutor를 상속받았기에 execute메서드와 ExecutorService자체에서 제공하는 submit 메서드, shutdown, shutdownNow, awaitTermination등의 메서드가 있음
## Method
### execute(Runnable command)
- Runnable한 인자를 받아 미래에 실행시킴
- void를 리턴함

### submit(Runnable command)
- execute와 마찬가지고러 Runnable한 인자와 Callable한 인자를 받아 미래에 실행시킴
- 인자의 수행 결과를 Future로 감싸서 리턴함

### awaitTermination(long timeout, TimeUnit unit)
- 시간을 인자로 받으며, 모든 작업이 끝나거나, 시간 초과되거나, 인터럽트가 발생할때까지 쓰레드를 block시킴

### shutdown()
- 이전에 제출된 작업은 유지하지만, 새로운 작업은 받지않음
- 제출된 작업이 완료되면 종료함

### shutdownNow()
- 이제