# autossh reverse tunnel
1. save ssh-tunnel.service in /etc/systemd/system
```ini
# ssh reverse tunnel

[Unit]
Description=Autossh reverse tunnel daemon
## make sure we only start the service after network is up
Wants=network-online.target
After=network.target

[Service]
Environment="AUTOSSH_GATETIME=0"
# ExecStart=/usr/local/bin/ssh-tunnel.sh
ExecStart=/usr/bin/autossh -o "ServerAliveInterval 30" -o "ServerAliveCountMax 100" -M 12022 -NR 2022:localhost:22 root@www.jumhorn.com -i /home/jumhorn/.ssh/id_rsa
ExecStop=pkill -9 autossh
User=jumhorn

[Install]
WantedBy=multi-user.target
```

2. start service
```shell
sudo systemctl start ssh-tunnel
```

# FAQ
* command analysis
	出问题时之行命令看输出结果分析
```shell
# ssh
ssh -o "ServerAliveInterval 30" -o "ServerAliveCountMax 100" -NR 2022:localhost:22 root@www.jumhorn.com -i /home/jumhorn/.ssh/id_rsa

#autossh
autossh -f -o "ServerAliveInterval 30" -o "ServerAliveCountMax 100" -M 12022 -NR 2022:localhost:22 root@www.jumhorn.com -i /home/jumhorn/.ssh/id_rsa
```