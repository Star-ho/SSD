---
created: 2024-01-04T22:47:40
updated: 2024-03-29T22:58
---
## Why?
- 클라이언트가 서버에게 http요청을 보내는 상황이 아닌, 서버에서 클라이언트에게 요청을 보내는 상황이 발생시 유용함
	- 서버에서 작업이 즉시 처리되지 않고, 처리되기까지 대기해야하는 상황
	- 서버에서 어떤 이벤트 발생 시 클라이언트에게 알려야 하는 상황
- 이를 위한 방안으로 polling, Long polling, streaming, web socket, plugin 등의 방안이 존재

## 자세한 내용은 RFC파일을 참고
- 당장 사용할 사항이 아니고, 단지 궁금증에 알아보는 것이니  이 문서에서는 간단하게 요약
> Long polling과 streaming은 [RFC6202](https://datatracker.ietf.org/doc/html/rfc6202)참고
> Web socket은 [RFC6455](https://datatracker.ietf.org/doc/html/rfc6455) 참고

## Pooling(폴링)

![[Pasted image 20240329225214.png|center|400]]
- 클라이언트가 주기적으로 서버에 요청을 보내서 확인하는 방식
- 클라이언트가 주기적으로 서버에 요청을 보내므로 서버의 변경에 즉시 대응하지 못함
- 다른 방법들은 서버에서 커넥션을 유지하고 있어야 하는 반면 폴링 방식에서는 커넥션을 유지하지 않아도 돼 서버에 부하가 적음

## Long polling(롱폴링)

![[Pasted image 20240329225407.png|center|600]]
- 클라이언트가 요청을 보내면, 서버에서 커넥션을 유지하다가 이벤트가 발생하면 응답하는 방식
- 폴링에 비해 실시간 처리가 가능함
- 서버가 여러번 응답을 해야 하는 상황에서는 효율이 좋지 않음
	- 서버가 응답을 한 후 클라이언트가 다시 요청해서 커넥션을 유지해야함



https://dydtjr1128.github.io/etc/2019/09/23/polling-long-polling-streaming.html
https://bcho.tistory.com/896
https://stackoverflow.com/questions/12555043/my-understanding-of-http-polling-long-polling-http-streaming-and-websockets

https://datatracker.ietf.org/doc/html/rfc6202
https://datatracker.ietf.org/doc/html/rfc6455


#long-polling
#Streaming
#Web-socket
