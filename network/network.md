# arp spoofing
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