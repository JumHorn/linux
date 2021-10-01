# linux

## shell

### su
```shell
# 发现进入root账户找不到sbin目录下的所有命令
# 使用su - 或者 su -l表示login shell继承环境变了PATH,PATH可以用export设置
su -l
```

### alias
```shell
# 设置alias将mac上命令不同的名字设置为linux下的名字
# alias ldd='otool -L'
# alias brew='HOMEBREW_NO_AUTO_UPDATE=1 brew'
alias ls='ls -F --color=auto'
alias grep='grep --color=auto'
```
### 命令后台运行
1. nohup
```shell
nohup command &
```
2. setsid
```shell
setsid command &
```
3. disown
```shell
disown -h %1
```
4. subshell
```shell
(command &)
```

### 命令前后台切换
1. 停止当前进程(ctrl + z)
2. 查看所有进程(jobs)
3. 切换到前台进程(fg)
4. 切换到后台进程(bg)
5. 演示例子
```shell
nc -lvp 1234 & # 命令后台执行
jobs # 查看后台执行命令编号
fg 1 # 将后台命令调到前台执行
ctrl + z # 停止当前进程
bg 1 # 将进程调到后台继续执行
```

### 命令历史查询
1. 查看历史命令
```shell
history
history 5 # the last 5 commands
```
2. 执行上一条命令
```shell
!!
!-1
```
3. 执行具体命令
```shell
!+命令编号
!445
```
4. even more
> https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps

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

4. 修改mac地址
```shell
# for MacOS
sudo ifconfig en0 ether d4:61:9d:32:3f:cf
```
```shell
# for linux
ip link set dev eth0 address XX:XX:XX:XX:XX:XX
```

5. 恢复默认mac地址
```shell
ethtool -P eth0
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

/media for system use \
/mnt for user use \
在debian上，如果mount到/media下的存储设备,gnome的filemanager是可以看到的
mount到其他位置上只有自己能看到

## enable/disable GUI
```shell
sudo systemctl set-default multi-user.target # disable GUI
sudo systemctl set-default graphical.target # enable GUI
```

## nmcli(network manager) 需要安装
> https://www.96boards.org/documentation/consumer/guides/wifi_commandline.md.html

1. 创建一个新的wifi连接
```shell
# 显示可以连接的无线网
nmcli dev wifi list
# 连接wifi
nmcli dev wifi connect SSID_Name password wireless_password
```
2. static IP
```shell
nmcli con modify con_name ipv4.method manual ipv4.address 192.168.10.155/24
```

3. 重启wifi
```shell
systemctl restart network-manager
```

3. 其他命令
```shell
# 显示子命令帮助
nmcli con -h
nmcli dev -h
# 显示本机所有连接
nmcli con show
# 启用连接
nmcli con up WiFi
nmcli general status
nmcli device status
```

## linux tty字体样式配置
```shell
sudo dpkg-reconfigure console-setup
```

## console locales(UTF8字符配置)
默认tty不能显示中文
```shell
# 安装
sudo apt-get install fbterm
# 启动
fbterm

# add to ~/.bashrc to automatically start
fbterm &>/dev/null
```

## usb device descriptor error -71

关机后再开机(重启无效)

## Tmux(terminal multiplexer)
terminal 分屏必用神器

1. 支持鼠标操作

~/.tmux.conf
```conf
set -g mouse on
```

2. Mac系统下复制内容

fn加鼠标拖动选中字符，然后正常cmd+c/cmd+v

## /proc
```shell
# 相关配置路径
/proc/sys/
# 随机端口范围
/proc/sys/net/ipv4/ip_local_port_range
# 文件fd最大值
/proc/sys/fs/file-max
```

## great tools
* glances
* sysbench
* pstack
* perf