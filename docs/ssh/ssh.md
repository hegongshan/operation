ssh，全称<strong style="color:red">s</strong>ecure <strong style="color:red">sh</strong>ell，是一种用于远程登录的协议。

语法：

```shell
ssh [options] user@hostname
```

选项：

`-p port`：指定端口号，默认为22；

`-i identity_file`：指定私钥文件。

示例：

这里以root用户和 IP 地址118.190.95.35（从网上随便找的一个IP）为例

```shell
ssh root@118.190.95.35
```

如果服务器的ssh端口号被修改过，假设修改后的端口号为1922，则需要添加-p选项：

```bash
ssh -p 1922 root@118.190.95.35
```
