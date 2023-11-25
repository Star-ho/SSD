## Architecture

![[Pasted image 20231125230312.png|center]]

### Server
- Server는 웹 컨테이너 자체를 의미
- 사용자가 거의 customize하지 않는 설정들의 기본 구현들을 제공

### Service
- Server내에있는 중간 구성 요소(intermediate component)로 하나 이상의 커넥터를 정확히 하나의 엔진과 연결시킴
- 기본 구현들이 간단하고 충분하므로, Server와 마찬가지로 사용자들이 거의 customize하지 않음

### Engine
- 특정 서비스에 대한 요청 처리 파이프라인을 나타냄
- Service는 여러 connector를 가질 수 있고, Engine은 이러한 커넥터로부터 온 모든 요청을 수신하고 처리하여, 클라이언트에 전달한 적절한 커넥터로 응답을 다시 전달함
- Engine 인터페이스는 사용자에 의해 구현될 수 있지만, 자주 발생하는 일은 아님

### Host





https://tomcat.apache.org/tomcat-9.0-doc/architecture/overview.html
https://medium.com/chequer/tomcat-spring-bootstrapping-sequence-1%ED%8E%B8-tomcat-4402102c0585