### Memory
- 고정값으로 설정
	- -Xmx(ex -Xmx4g)
		- 최대값
	- -Xms(ex -Xms500m)
		- 최소값
- 비율로 설정
	- -XX:MaxRAMPercentage(-XX:MaxRAMPercentage=75),
		- 최대값
	- -XX:InitialRAMPercentage(-XX:InitialRAMPercentage=75)
		- 최소값
- 메모리 설정시 팁!
	- container메모리와 heap은 같은 사이즈로 가면 안됨
		- java에는 heap말고 non-heap도 있기때문
		- 컨테이너 메모리와 같은 크기로 했을 때 컨테이너도 crash 발생하기 때문에 oom 후처리가 안됨
	- percentage로 75%정도 권장
		- [ms홈페이지 참고](https://learn.microsoft.com/en-us/azure/developer/java/containers/overview)
		- 물론 절대적인건 아님
	- 하나의 컨테이너에 하나의 어플리케이션만 돌아갈떄 min size와 max size를 같게 설정
		- 메모리가 부족이 발생하면 os에 메모리를 더 달라고 요청하는데, 어차피 하나의 컨테이너에 하나의 프로세스만 돌아가는데 굳이 필요없는 요청을 늘릴 필요가없음
		- gc가 더 자주 실행됨
		- 하나의 컨테이너에서 하나의 프로세스만 돌기 때문에 경쟁이 필요가 없음
### OOM 처리
- -XX:+HeapDumpOnOutOfMemoryError
- -XX:HeapDumpPath=/var/run/tpirates/$BUILD_TARGET
### MaxRAMFraction 옵션 찾아보기


#wait-to-update 
https://learn.microsoft.com/en-us/azure/developer/java/containers/overview
https://stackoverflow.com/questions/43651167/is-there-any-advantage-in-setting-xms-and-xmx-to-the-same-value
https://developer.jboss.org/thread/149559
https://www.codementor.io/@suryab/outofmemoryerror-related-jvm-arguments-w6e4vgipt
https://medium.com/nordnet-tech/setting-java-heap-size-inside-a-docker-container-b5a4d06d2f46
https://dzone.com/articles/best-practices-java-memory-arguments-for-container