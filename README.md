# linux

## shell

## daemon

When a daemon starts up, it has to do some low-level housework to get itself ready for its real job

1. Fork off the parent process(init process with pid 0 is the new parent)
2. Change file mode mask (umask)
3. Open any logs for writing
4. Create a unique Session ID (SID)
5. Change the current working directory to a safe place
6. Close standard file descriptors
7. Enter actual daemon code

### manager services(systemctl)

```shell
sudo systemctl disable geoclue.service
sudo systemctl mask geoclue.service # prohibit to /dev/null
```

## network

1. remove virtual network interface
```shell
sudo ip link set dev outline-tun0 down
```

2. edit host file
```shell
# edit this file
vim /etc/hosts
```

3. nslookup(name server lookup)
```shell
# debian should install dnsutils
sudo apt install dnsutils
```

## package management(apt/yum)

> https://www.debian.org/doc/manuals/debian-reference/ch02.en.html

## permissions

* root用户也无法删除只读文件，所以要先修改权限
* root用户无法删除挂载的只读文件,修改权限也无法在挂载的文件上实现,要找到原文件的位置
```shell
# 执行mount命令,查看所有挂载
mount
```

## /mnt vs /media

/media for system use
/mnt for user use
在debian上，如果mount到/media下的存储设备,gnome的filemanager是可以看到的
mount到其他位置上只有自己能看到

## enable/disable GUI
```shell
sudo systemctl set-default multi-user.target # disable GUI
sudo systemctl set-default graphical.target # enable GUI
```

## wpa_cli
1. wpa_cli交互模式
```shell
sudo wpa_cli
# 查找网络
scan
# 显示查找结果
scan_results
#
add_network
#
set_network 1 ssid "network_name"
set_network 1 psk "passwd"
list_networks
enable_network 1
select_network 1
save_config
dhcpcd eth0
```
2. wpa_cli非交互模式
```shell
# 单引号必须要
sudo wpa_cli set_network 1 ssid '"network_name"'
sudo wpa_cli set_network 1 psk '"passwd"'
sudo wpa_
```

## nmcli(network manager)
> https://www.96boards.org/documentation/consumer/guides/wifi_commandline.md.html

1. 创建一个新的wifi连接
```shell
# 用wifi名做连接名即可
nmcli con add con-name WiFi ifname wlan0 type wifi ssid foonet
# 输入密码
nmcli con modify WiFi wifi-sec.key-mgmt wpa-psk
nmcli con modify WiFi wifi-sec.psk myownpassword
# 启用连接
nmcli con up WiFi
```

2. 其他命令
```shell
# 显示可以连接的无线网
nmcli dev wifi list
# 显示本机所有连接
nmcli con show
nmcli general status
nmcli device status
```