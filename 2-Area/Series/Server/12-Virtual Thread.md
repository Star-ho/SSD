
## Platform Thread
![[Pasted image 20231223233300.png]]


## Virtual Thread
![[Pasted image 20231223233244.png]]

## 비교
![[Pasted image 20231223233119.png]]

버추얼 쓰레드가 블럭킹 되면
- 해당하는 코드 찾기
버추얼 쓰레드 스케줄링이 
기존 쓰레드 언마운트하고
다른 캐리어 쓰레드로 연결해줌

쓰레드를 heap에 저장하면 터지진 않을까?

### 유의사항
- CPU bound한 상황에서는 Platform Thread가 더 나은 성능을 보여줌
- 정말 스트리밍 데이터를 사용한다면 reactor를 고려하자
- syncronized 또는 JNI call 시  carrier thread에 블로킹(pinning)이 발생
	- syncronized을 reenterantLock으로 변경
- thread local을 사용시 메모리가 터질 수 있음

https://techblog.woowahan.com/15398/
https://tech.kakao.com/2023/12/22/techmeet-virtualthread/
https://medium.com/deno-the-complete-reference/springboot-virtual-threads-vs-webflux-performance-comparison-for-jwt-verify-and-mysql-query-ff94cf251c2c

https://www.diva-portal.org/smash/get/diva2:1763111/FULLTEXT01.pdf

https://docs.oracle.com/en/java/javase/20/core/virtual-threads.html#GUID-2BCFC2DD-7D84-4B0C-9222-97F9C7C6C521

https://blog.rockthejvm.com/ultimate-guide-to-java-virtual-threads/

https://github.com/brettwooldridge/HikariCP/issues/2151 

https://perfectacle.github.io/2022/12/29/look-over-java-virtual-threads/

#가상쓰레드
#java
#virtual-thread
#lock