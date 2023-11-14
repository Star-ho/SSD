왜 linux service인가?
장점


```
# vi /etc/systemd/system/testchk.service

// /etc/systemd/system/testchk.service 내용
[Unit]
Description=Systemd Test Daemon

[Service]
Type=simple
ExecStart=/root/test-daemon.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

#wait-to-update 