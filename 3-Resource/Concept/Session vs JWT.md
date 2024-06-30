---
date: 2024-06-30 17:12:18
updatedAt: 2024-06-30 17:12:25
---
## Session
- 웹 서비스에서 사용자의 정보를 저장하고 있는 곳
- 사용자에게는 SessionId를 넘겨주고, 해당 세션 ID를 통해 사용자의 정보를 접근
- 사용자가 접근시마다 session 정보를 확인해야 하기 때문에 부하가 발생함

## JWT
- 사용자의 정보를 jwt Token에 저장하는 방법
- 사용자에게 해당 토큰을 줌
- 토큰 내에는 서비스에서 필요하다고 생각되는 정보가 들어가있음
- 토큰 발행, 검증시 비밀번호를 사용해서 검증하기 때문에, 



https://www.tcpschool.com/php/php_cookieSession_session#google_vignette