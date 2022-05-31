在CentOS中，网络启动相关配置存放在目录`/etc/sysconfig/network-scripts`中：

```bash
cd /etc/sysconfig/network-scripts
```

查看目录下形如`ifcfg-xxx`的文件

```bash
cat ifcfg-enp2s0f0
```

BOOTPROTO：启动协议（**Boot Proto**col）

* none

* static：固定IP

* dhcp：Dynamic Host Configuration Protocol，动态主机配置协议，动态分配IP

ONBOOT：是否开机启动

* no：开机不自动启动

* yes：开机自动启动

### 实验过程

1.修改网络配置

```bash
IPADDR=192.168.255.101
GATEWAY=192.168.255.2
NETMASK=255.255.255.0
DNS=192.168.255.1
```

2.配置DNS

```bash
[root@hgs ~]# echo nameserver 8.8.8.8 > /etc/resolv.conf
[root@hgs ~]# echo nameserver 114.114.114.114 > /etc/resolv.conf
```

3.重启网络服务

```bash
[root@hgs ~]# systemctl restart network
```

查看网络状态

```bash
[root@hgs ~]# systemctl status network
```

4.查看本机的IP地址

```bash
[root@hgs ~]# ifconfig
```

不出意外的话，输出的IP地址将与文件`/etc/sysconfig/network-scripts/ifcfg-enp2s0f0`中配置的IP地址一致。

5.测试网络连通性

```bash
ping www.baidu.com
```

如果找不到ping命令：

```bash
bash: ping: command not found
```

则需要安装iputils库

```bash
yum install -y iputils
```

