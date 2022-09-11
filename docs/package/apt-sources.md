在使用APT服务时，网络延迟比较大，当包较大时，问题尤为明显。此时，可以使用国内的镜像，体验飞一般的速度。

1.安装HTTPS认证包

```bash
apt install -y ca-certificates
```

2.备份当前的源（后悔药）

```bash
cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

3.修改软件源配置文件

```bash
vim /etc/apt/sources.list
```

以清华的镜像为例，将原生的`cn.archive.ubuntu.com`替换为`mirrors.tuna.tsinghua.edu.cn`

```bash
:%s/http:\/\/cn.archive.ubuntu.com/https:\/\/mirrors.tuna.tsinghua.edu.cn/g
```
