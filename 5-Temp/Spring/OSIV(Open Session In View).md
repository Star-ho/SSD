---
date: 2024-05-07 17:35:56
updatedAt: 2024-05-07 17:36:29
---
https://junhyunny.github.io/spring-mvc/jpa/open-session-in-view/

정리한번하기

osiv가 켜져있으면, 커넥션 반납을 dispatcher servlet직전에 반납
트랜잭션이 끝나고 반납하는게 아닌, api요청이 완전히 끝나야 반납함

#wait-to-update 