# tshark常用命令

1. 查看所有设备
```shell
tshark -D
```

2. 选择要监视的设备
```shell
tshark -i 设备编号
```

3. 显示模式
```shell
# -x表示16进制显示
```

4. 监视类型
```shell
# -f选项表示监视类型
sudo tshark -f "udp port 8000" -i 8 -x
```

5. 只显示报文内容
```shell
# -T fields -e data
sudo tshark -f "udp port 8000" -i 7  -T fields -e data
```

6. 保存数据包到文件
```shell
tshark -P -i eth0 -f "host 192.168.31.33" -w /tmp/eth0.pcap
```