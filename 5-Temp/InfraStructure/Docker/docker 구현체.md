---
created: 2024-01-19T22:56:48
date: 2024-03-03T11:41
updated: 2024-03-31T22:43
---
리눅스 컨테이너는 운영체제 커널을 제외한 모든 프로세스와 독립적인 1개의 프로세스를 실행하는 기술이며, 프로세스 단위로 독립된 환경에서 실행되며, 구현하려면 시스템 콜인 chroot나 namespace, cgroup,union mount를 활용해야 된다고 하는데

윈도우에서 도커는 어떻게 구현될까 갑자기 궁금해졌습니다

linuxKit을 씁니당

그럼 MacOS는 어떻게 되어있을까?!

리눅스 환경이니까 리눅스랑 똑같이 동작할까?! 라고 생각해보면

사실 이 친구도 linuxKit을 씁니다

https://selog.tistory.com/entry/%EA%B0%80%EC%83%81%ED%99%94-%EA%B0%80%EC%83%81%EB%A8%B8%EC%8B%A0VM%EA%B3%BC-%ED%95%98%EC%9D%B4%ED%8D%BC%EB%B0%94%EC%9D%B4%EC%A0%80-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0