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