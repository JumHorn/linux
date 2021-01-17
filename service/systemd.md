# autossh reverse tunnel
1. service config in /etc/systemd/system
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
ExecStart=/usr/bin/autossh -o "ServerAliveInterval 30" -o "ServerAliveCountMax 100" -M 12022 -NR 2022:localhost:22 root@81.69.226.177 -i /home/jumhorn/.ssh/id_rsa
ExecStop=pkill -9 autossh
User=jumhorn

[Install]
WantedBy=multi-user.target
```