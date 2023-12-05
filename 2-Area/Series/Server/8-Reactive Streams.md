- 논블로킹 배압(back pressuer)을 사용한 비동기 스트리밍 처리를 위한 표준
- network protocol 뿐만아니라 JVM, Javascript와 같은 런타임 환경에 대한 표준도 포함함
- 스트림 데이터라고도 표현되는 크기가 정해지지 않은 'live'데이터는 비동기 시스템에서 주의가 필요함
	- 들어오는 데이터가 처리되는 속도보다 빠르면 안되기 때문
		- 데이터가 많으면 쌓이고, 그러다 보면 메모리가 터지기때문
- 



https://www.reactive-streams.org/
https://github.com/reactive-streams/reactive-streams-jvm/blob/v1.0.4/README.md팅