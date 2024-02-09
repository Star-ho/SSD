
작업
1. a에 요청 
   	- 리스폰스 A
2. b에 요청 
	- 리스폰스 B
3. a와 b를 합쳐서 -> Z요청을 만듬
4. 1요청을 c에전송해서 리스폰스 C를 받고 리턴

---- reactor java

코드
val a: MONO<A>=webclient.get("a")
	.bodyToMono(A.class)

val b: MONO<B> =webclient.get("b")
	.bodyToMono(B.class)

val z:Z = Mono.zip(a,b)

val c:Mono<C> = webclient.get("c")

return c

상세
1. A에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- 리스폰스 생성

2. B에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- 리스폰스 생성

3.C를 보내기전에 reactor에서도 wait가 필요 


---- coroutine

코드 
val a: A=webclient.get("a")
	.bodyToMono(A.class)

val b: B =webclient.get("b")
	.bodyToMono(B.class))

val z:Z = Z(a.await(),b.await())

val c:C = webclient.get("c").awaitSingle()

상세
1. A에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- 리스폰스 생성

2. B에 요청하는 publisher생성 후 요청보냄
- selector에 등록
- selector에서 리스폰스 오면 subscriber에게 알림
- 리스폰스 생성

- continuation 결과를 기존 로직을 실행하는 (쓰레드?)에 '전달'함

3.C를 보내기전에 reactor에서도 wait가 필요 


io dispatcher에도 selector가 있어
send만 하고 다른 클라이언트로 스위칭 하는지?



