---
created: 2024-01-04T22:47:40
updated: 2024-03-29T22:48
---
## Why?
- 클라이언트가 서버에게 http요청을 보내는 상황이 아닌, 서버에서 클라이언트에게 요청을 보내는 상황이 발생시 유용함
	- 서버에서 작업이 즉시 처리되지 않고, 처리되기까지 대기해야하는 상황
	- 서버에서 어떤 이벤트 발생 시 클라이언트에게 알려야 하는 상황
- 이를 위한 방안으로 polling, Long polling, streaming, web socket, plugin 등의 방안이 존재

### Long polling과 streaming은 RFC6202에


https://dydtjr1128.github.io/etc/2019/09/23/polling-long-polling-streaming.html
https://bcho.tistory.com/896

https://datatracker.ietf.org/doc/html/rfc6202
https://datatracker.ietf.org/doc/html/rfc6455


#long-polling
#Web-socket
