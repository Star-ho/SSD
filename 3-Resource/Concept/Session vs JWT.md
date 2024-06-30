---
date: 2024-06-30 17:12:18
updatedAt: 2024-06-30 17:12:25
---
## Session과 JWT
- stateless한 웹서버에서, 로그인한 사용자의 정보를 저장하는 방식

## Session
- 웹 서비스에서 사용자의 정보를 서버내 어떤곳에 저장하고 사용자에게는 Session ID를 발급함
	- 세션 내에는 사용자의 정보와 Session ID가 있음
- 사용자의 세션 ID를 통해 사용자의 정보를 접근
- 사용자가 접근시마다 session 정보를 확인해야 하기 때문에 부하가 발생함

## JWT
- 사용자의 정보를 jwt Token에 저장하는 방법
- 사용자에게 해당 토큰을 줌
- 토큰 내에는 사용자의 정보가 들어가있음(ID, 권한 등)
- 토큰 발행, 검증시 시크릿키를 사용하기 때문에 시크릿 키를 모르면, 임의 조작이 불가능함
- jwt탈취 문제가 발생할 수 있음
	- 탈취 문제를 방지하기 위해 black list token을 발급하거나, token의 타임아웃 시간을 짧게 가져가는 방법이 있음


https://www.tcpschool.com/php/php_cookieSession_session#google_vignette