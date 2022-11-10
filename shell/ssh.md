# ssh

	ssh技巧，解释使用方法，了解这最好的工具

## 基本使用
* 免密码登录

1. ssh-keygen
```shell
ssh-keygen -t rsa -C "email"
```

2. ssh-copy-id user@ip_address

* 允许特定用户密码登录

	编辑/etc/ssh/sshd_config
```
Match User <username>
PasswordAuthentication yes
Match all
```

## ssh隧道
	ssh用作代理的4种模式命令
1. 从client端口访问server端口
```shell
ssh -L [localhost]:localport:serverhost:serverport username@serverhost
```
2. 从server端口访问client端口
```shell
ssh -R [serverhost]:serverport:localhost:localport username@serverhost
```
3. 用server代理client访问外网(socks)
```shell
ssh -D [localhost]:localport username@serverhost
```
4. 用client代理server访问内网(socks)
```shell
ssh -R [serverhost]:serverport username@serverhost
```

## 其他参数
1. -N 不执行命令，仅代理端口
2. -f 后台运行
3. -C 数据压缩

## 例子
* reverse ssh tunnel(反向连接)
```shell
# local host
ssh -fCNR 2022:localhost:22 root@remoteIP
```
```shell
# remote host
ssh root@localhost -p 2022
```
* 反向链接网关配置

允许外网连接配置,需要反向代理开放端口的机器上配置/etc/ssh/sshd_config
```config
GatewayPorts yes
```

## autossh

	ssh挂掉后重新连接
```shell
# not stable
autossh -M 12022 -fNCR 2022:localhost:22 root@remoteIP
```
```shell
autossh -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -M 12022 -fNCR 2022:localhost:22 root@remoteIP
```