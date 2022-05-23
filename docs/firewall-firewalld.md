firewall-cmd是CentOS的默认防火墙。默认禁止所有访问。

* 启动防火墙

```bash
systemctl start firewalld
systemctl enable firewalld
```

* 开放某个端口

```bash
firewall-cmd --permanent --zone=public --add-port=1922/tcp
```

* 重新加载防火墙

```bash
firewall-cmd --reload
```

* 查看开放的所有端口

```bash
firewall-cmd --permanent --zone=public --list-ports
```

* 关闭已开放的端口

```bash
firewall-cmd --permanent --zone=public --remove-port=1922/tcp
```

* 关闭防火墙

```bash
systemctl stop firewalld
systemctl disable firewalld
```
