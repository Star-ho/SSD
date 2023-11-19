핵심은 continueos passing style

코루틴의 코드들은 cps 스타일로 바뀌며, delay가 발생했을때 해당 메서드를 리턴하고 다음 메서드를 실행
- 경험적

여기서 reactive streamse랑 어떻게 호환되는지
- https://huisam.tistory.com/entry/webflux-coroutine
- await가 subscibe와 같이 동작

reactor netty에서 어떤상황에서 쓰레드가 변경되는지 확인해야함
- subscribe할때

webflux 에서 임의의 클래스에서 request정보 받아오기
- https://velog.io/@slolee/ThreadLocal-%EC%82%AC%EC%9A%A9%EC%8B%9C-%EC%A3%BC%EC%9D%98%ED%95%A0%EC%A0%90

- 스레드와 스케줄러 알아보기
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sthwin&logNo=221956619428


#wait-to-update 
#argent