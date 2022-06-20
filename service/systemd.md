# systemd

	linux system service

## create .service file

	there are two path to store the service file   \

* /etc/systemd/system vs /lib/systemd/system
```shell
man systemd.unit
# /etc/systemd/system 用户配置文件
# /lib/systemd/system (apt/yum/pacman)
```

## normal use
```shell
systemctl start service_name
systemctl stop service_name
systemctl status service_name
systemctl restart service_name
systemctl reload service_name
```

## auto start service
```shell
systemctl enable service_name
# see it is list in install target
ls -l /etc/systemd/system/multi-user.target.wants/*.service
```

## disable service
```shell
systemctl disable service_name
```

## example

1. autossh
2. frp