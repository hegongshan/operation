### 什么是IPMI

IPMI，全称为Intelligent Platform Management Interface，智能平台管理接口。

### 安装IPMI管理工具

```shell
# CentOS
yum install -y ipmitool

# Ubuntu
apt install -y ipmitool
```

### 远程登录

```shell
ipmitool -H <address> -U <username> -P <password> shell
```

例如：

```shell
[root@hgs ~]$ ipmitool -H 127.0.0.1 -U admin -P admin shell
```

### 开关机

```shell
ipmitool> power on
ipmitool> power off
```

### 退出登录

使用`exit`或者`quit`，可以退出登录。

```shell
ipmitool> exit
ipmitool> quit
```

