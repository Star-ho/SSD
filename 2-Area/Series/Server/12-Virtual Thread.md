
가상쓰레드
virtual Thread

버추얼 쓰레드가 블럭킹 되면
버추얼 쓰레드 스케줄링이 
기존 쓰레드 언마운트하고
다른 캐리어 쓰레드로 연결해줌

쓰레드를 heap에 저장하면 터지진 않을까?

유의사항
- syncronized시 carrier

https://techblog.woowahan.com/15398/
https://tech.kakao.com/2023/12/22/techmeet-virtualthread/
https://medium.com/deno-the-complete-reference/springboot-virtual-threads-vs-webflux-performance-comparison-for-jwt-verify-and-mysql-query-ff94cf251c2c

https://www.diva-portal.org/smash/get/diva2:1763111/FULLTEXT01.pdf

https://docs.oracle.com/en/java/javase/20/core/virtual-threads.html#GUID-2BCFC2DD-7D84-4B0C-9222-97F9C7C6C521

https://blog.rockthejvm.com/ultimate-guide-to-java-virtual-threads/

https://github.com/brettwooldridge/HikariCP/issues/2151 

https://perfectacle.github.io/2022/12/29/look-over-java-virtual-threads/


#java
#virtual-thread
#lock