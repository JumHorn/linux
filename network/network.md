# arp spoofing
## MacOS
1. 开启IP转发
```shell
# Linux
echo 1 >/proc/sys/net/ipv4/ip_forward
# Mac
sudo sysctl -w net.inet.ip.forwarding=1
```
2. 查看IP转发
```shell
sudo sysctl -a | grep forward
```