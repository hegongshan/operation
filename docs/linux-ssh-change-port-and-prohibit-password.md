处于安全考虑，需要修改服务器的SSHD端口号，并禁止密码登录。


### 生成key

1.在个人电脑中，使用RSA算法生成公钥和私钥：

```bash
ssh-keygen -t rsa -f root@2.84
```

![生成公钥和私钥](/img/ssh-generate-key.png)

将公钥发送给服务器（公钥文件名后缀`.pub`可加可不加，不加会自动加上）：

```bash
ssh-copy-id -i root@2.84.pub root@10.190.2.84
```

![将公钥发送给服务器](/img/ssh-copy-key.png)

### 配置sshd

1.登录服务器，修改sshd_config文件：

```bash
vim /etc/ssh/sshd_config
```

将Port的值修改为需要使用的端口（如1922），取消`PubkeyAuthentication`的注释，并修改`PasswordAuthentication`的值：

```bash
Port 1922

PubkeyAuthentication yes

PasswordAuthentication no
```

### 配置SELinux

1.在SELinux（Security-Enhanced Linux）中为sshd添加1922端口

```bash
semanage port -a -t ssh_port_t -p tcp 1922
```

2.确认添加是否成功

```bash
semanage port -l | grep ssh_port_t
```

![确认添加是否成功](/img/ssh-selinux-add-port.png)

### 配置防火墙

1.查看防火墙状态：

```bash
systemctl status firewalld
```

2.如果没有开启，则启动防火墙：

```bash
systemctl start firewalld
systemctl enable firewalld
```

3.开放端口

```bash
firewall-cmd --permanent --zone=public --add-port=1922/tcp
firewall-cmd --reload
```

![开放端口](/img/ssh-firewall-add-port.png)

### 测试

1.服务器：重启sshd

```bash
systemctl restart sshd
```

2.客户端：尝试使用默认22端口登录

![使用默认端口登录](/img/ssh-try-login-connection-refused.png)

3.客户端：使用正确的端口，尝试使用密码登录

![使用密码登录](/img/ssh-try-login-permission-denied.png)

4.客户端：使用正确的端口和秘钥进行登录

```bash
ssh -p 1922 -i root@2.84 root@IP
```

![正确登录](/img/ssh-try-login-success.png)
