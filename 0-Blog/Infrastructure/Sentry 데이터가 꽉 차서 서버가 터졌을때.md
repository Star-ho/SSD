---
created: 2023-10-02T23:13:36
updated: 2024-03-08T23:19
---
sentry가 올라가있는 인스턴스의 저장공간이 꽉참

![[Pasted image 20231002231423.png]]

현재 리텐션 주기가 90일인데, 90일치를 다 저장하기에는 200G가 모자란 상황

- 어플리케이션 수가 늘어나거나, 리텐션 기간이 늘어날때는 용량조정 필요
- 일주일정도 용량 체크하면서 얼마나 쌓이는지 확인 필요
- **적당한 용량 확인 디스크 크기 변경할것**

postgresql이 sentry의 메인저장소
postgresql의 nodestore_node테이블은 수집한 raw데이터가 저장되는곳
nodestore_node테이블의 로우가 5000만건 존재 - 165G를 차지
sentry에서 조회하는 데이터는 nodestore_node데이터를 가공해서 따로 저장
nodestore_node테이블은 정리가 가능!

[참고링크](https://develop.sentry.dev/self-hosted/troubleshooting/#postgres)

아래의 명령어로 데이터 정리가 가능하다

```shell
vacuum full nodestore_node;
vacuum full;

/**
* vacuum
*	- 쓰레기 데이터 정리
*
*/

```

```shell
날짜 이후로 데이터 삭제
delete from nodestore_node where timestamp < '2023-07-13';
```

위의 문제가 있었다면 nignx buffer pool, zookeeper쪽 문제가 있을거라

아래의 도커 볼륨을 삭제

```c
sentry-self-hosted_sentry-nginx-cache
sentry-self-hosted_sentry-zookeeper-log
sentry-self-hosted_sentry-kafka-log
sentry-zookeeper
sentry-kafka
```

이후 sudo ./install.sh 초기세팅해주고

```shell
sudo docker-compose up -d
```


로 센트리를 실행하면 된다