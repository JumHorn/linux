# touch filename
1. 创建文件 \
该命令在windows下的bash命令行里可以使用。可以方便的在windows下创建以.开始的文件名的文件
2. 修改文件时间戳
> touch -c filename

不创建文件，为已经存在的文件加上最新的时间戳，在编译时可以不改动文件，使得make命令重新编译

# find
1. 查找文件 \
find / -name RegularExpressions
2. 排除权限不足文件 \
find / -name git 2>/dev/null

# whereis
查找命令的帮助文档和二进制文件
> whereis git

# locate
类似于everything建立数据库来查找

# grep
1. 查找文件内容
> grep -rn test ./ --include=*.cpp

递归查找当前目录下的所有cpp文件中包含test的行，并打印行号

2. grep管道
搜索大多数命令的结果
> ps -A | grep firewalls

# clear command line
* clear current line \
ctrl + u
* clear all
cls for Dos and clear for linux/Mac \
or shortcut ctrl + l

# ssh
免密码登录

* ssh-keygen
ssh-keygen -t rsa -C "some content(git example gmail)"

* ssh-copy-id user@ip_address

# stat
查看文件inode和链接信息
> stat filename \

# netstat
查看端口和进程pid信息
> netstat -ap | grep port/pid/name

# route
查看路由信息 \
route get default

# scp
scp [参数] [原路径] [目标路径]
1. 传输文件 \
scp local_file remote_username@remote_ip:remote_folder
2. 传输文件夹 \
scp -r local_folder remote_username@remote_ip:remote_folder

# tar
> https://www.tecmint.com/18-tar-command-examples-in-linux/

* 压缩文件 \
c – Creates a new .tar archive file. \
v – Verbosely show the .tar file progress. \
f – File name type of the archive file \
例子 \
路径要是相对路径 \
tar cvf[z] compressedfilename directory \
压缩等级 z是gzip j是tar.bz2更高 没有表示不压缩 \

* 解压缩 \
tar xvf compressedfilename -C directory
x表示解压缩

* 查看压缩文件内容 \
tar tvf compressedfilename \
t表示listcontent

# awk

# 路径切换
1. 回到家目录
> cd ~ 或者直接cd即可
2. 回到前一次路径
> cd -

# 执行shell脚本
1. sh执行shell脚本 \
会新建一个子shell
2.  在当前shell下执行脚本 \
source filename
相当于. filename之间有空格

# && || 命令
command1 && command2 表示command1执行成功后再执行command2 \
||表示command1执行失败后再执行command2

# ip与mac地址配置
1. ip addr添加和删除ip \
ip addr add 192.168.1.3/24 dev eth0 \
ip addr del 192.168.1.3/24 dev eth0 \

2. ifconfig修改ip \
ifconfig eth0 192.168.1.3/24 up \
ifconfig eth0 192.168.1.3/24 down \

3. ipconfig修改mac地址 \
ifconfig eth0 hw ether 10:81:84:00:10:06

# 生成文件md5
> md5sum -b filename

相关命令sha256sum，sha512sum

# shell 重定向
1. ps 看到设备名
pts/0 bash \
pts/0 ps

2. 设备都在dev/pts下 \
echo string > /dev/pts/1

3. 特殊情况 \
qDebug输出在stderr上 \
所以使用 ./program 2 > /dev/pts/0 \
例子./program 2>/dev/pts/0 1> /dev/pts/0 2 > /dev/pts/0

# 远程启动带界面程序
oli@bert:~$ ssh tim@ip \
oli@tim:~$ export DISPLAY=:0 \
oli@tim:~$ firefox \