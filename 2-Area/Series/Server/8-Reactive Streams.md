## 개념
- 논블로킹 배압(back pressuer)을 사용한 비동기 스트리밍 처리를 위한 표준
- network protocol 뿐만아니라 JVM, Javascript와 같은 런타임 환경에 대한 표준도 포함함
- 스트림 데이터라고도 표현되는 크기가 정해지지 않은 'live'데이터는 비동기 시스템에서 주의가 필요함
	- 들어오는 데이터가 처리되는 속도보다 빠르면 안되기 때문
		- 데이터가 많으면 쌓이고, 그러다 보면 메모리가 터지기때문
- Reactive Streams의 주요 목표는 비동기 경계를 넘은 데이터 스트림의 교환(데이터를 다른쓰레드 혹은 쓰레드 풀로 전달하는)하며 수신측에서는 임의의 데이터양을 버퍼로 관리하지 않는것임
- backpressure는 스레드 사이의 대기열을 제한하기 위한 필수적인 부분임
- 또한 백프레셔 신호가 동기식일 경우 비동기 처리의 이점이 없어지기에, Reactive Streams의 구현은 모든측면에서 비차단, 비동기식으로 구성되도록 주의를 기울임

## 구성요소
### Publisher
- 잠재적으로 무한한 수의 시퀀스 요소를 제공
- Subscriber의 요청을 받으면 publishing을 시작함



https://www.reactive-streams.org/
https://github.com/reactive-streams/reactive-streams-jvm/blob/v1.0.4/README.md팅