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
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

#wait-to-update 