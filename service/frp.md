# prepare
1. copy config file to /etc/frp
2. copy execute file to /usr/local/bin

# frpc client service
1. save frpc.service in /etc/systemd/system
```ini
[Unit]
Description=Frp Client Service
After=network.target

[Service]
Type=simple
User=nobody
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/frpc -c /etc/frp/frpc.ini
ExecReload=/usr/local/bin/frpc reload -c /etc/frp/frpc.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

2. start service
```shell
systemctl enable frpc
systemctl start frpc
```

# frps server service
1. save frps.service in /etc/systemd/system
```ini
[Unit]
Description=Frp Server Service
After=network.target

[Service]
Type=simple
User=nobody
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/frps -c /etc/frp/frps.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

2. start service
```shell
systemctl enable frps
systemctl start frps
```