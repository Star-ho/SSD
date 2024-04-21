---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:23:53+5340
---
gc가 뭔지  
어떻게 이루어지는지  
stop the world?  
gc의 종류  
종류별 장단점  
어떤상황에서 어떤 gc를 쓰면 좋은지?  
gc로그 보기 (gceasy.io)


Garbage collection 이 있는 언어를 원자력 발전소, 자동차 동력 제어, 인공위성, 국가 전력망 제어시스템 같은 곳에 쓸 수 있을까요? 후보자님의 생각을 말씀해 주세요.

흠냐 gc의 단점은 생각해 보면
1. stw
2. 바로 초기화 안 하니까 그 사이에 누수 발생할 수 있음
3. 알고리즘 잘못되어도 누수 발생 가능

gc
참조를 읽은 객체를 메모리에서 제거하는거
miner gc - young 영역의 객체를 제거
major gc - old 영역의 객체를 제거

https://stackoverflow.com/questions/16695874/why-does-the-jvm-full-gc-need-to-stop-the-world
https://d2.naver.com/helloworld/0128759
https://mirinae312.github.io/develop/2018/06/04/jvm_gc.html


https://d2.naver.com/helloworld/1329

https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html