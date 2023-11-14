왜 linux service인가?
장점


```
# vi /etc/systemd/system/testchk.service

// /etc/systemd/system/testchk.service 내용
[Unit]
Description=Systemd Test Daemon

[Service]
Type=simple
ExecStart=java -jar /root/ktx-cron/build/libs/ktx-cron-1.0-SNAPSHOT.jar
Restart=always

[Install]
WantedBy=multi-user.target
```
https://passwd.tistory.com/entry/Ubuntu-Systemd-service-%EB%93%B1%EB%A1%9D


#wait-to-update 