1. 요청
2. 메모리 -> buffer
- socket buffer? kernel buffer?
3. tcp hand shake
4. sendbuffer
5. 네트워크 지연시간
6. recv buffer
- socket buffer? kernel buffer?
- recv buffer에 있는걸 kernel buffer에도 옮겨야할지?
7. 쓰레드 받고
8. 메모리에 올라가고
9. 요청 처리(web server, db, etc...)
10. 1-8과정 반복

네트워크 인터페이스 카드에서 하는건 뭔지?
https://stackoverflow.com/questions/53691760/what-are-the-differences-between-kernel-buffer-tcp-socket-buffer-and-sliding-wi
참고


#argent 