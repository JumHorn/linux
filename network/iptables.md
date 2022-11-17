# iptables

	Linux Firewall
	三条规则INPUT FORWARD OUTPUT
	三种方法Accept Drop Reject

## 查看系统iptable
```shell
iptables -L -v
```

## 拒绝连接
```shell
# A append chain
# s source address
# jump target

iptables -A INPUT -s 10.10.10.10 -j DROP # drop connection from ip
iptables -A INPUT -s 10.10.10.0/24 -j DROP # drop connection from ip range
iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -j DROP # block SSH connections from ip
```

## 删除规则
```shell
iptables -D INPUT -s 10.10.10.10 -j DROP # same command as append

# or use number
iptables -L --line-numbers
iptables -D INPUT 3 # delete specific chain number
```

## 保留更改
```shell
# debian

# arch linux
iptables-save -f /etc/iptables/iptables.rules
```