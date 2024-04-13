---
created: 2024-03-31T22:41:00
date: 2024-04-13T22:56
---
왜 linux service인가?
장점
- 꺼져도 다시 살아남
# service파일 생성
```
vi /etc/systemd/system/ktx.service
```

```
# /etc/systemd/system/ktx.service 내용
[Unit]
Description=Systemd Test Daemon

[Service]
Type=simple
ExecStart=java -jar /root/ktx-cron/build/libs/ktx-cron-1.0-SNAPSHOT.jar
Restart=always
RuntimeMaxSec=1d
```

```

[Install]
WantedBy=multi-user.target

```

서비스 실행
```
systemctl daemon-reload

systemctl enable ktx.service

service ktx start

service ktx status

## restart시 jar변경내용 적용됨
service ktx restart
```
https://passwd.tistory.com/entry/Ubuntu-Systemd-service-%EB%93%B1%EB%A1%9D


#wait-to-update 