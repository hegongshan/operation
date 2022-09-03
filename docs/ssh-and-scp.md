Linux中使用**ssh命令**登录其他的Linux，使用**scp命令**实现文件传输。

<!--more-->

### ssh

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

### scp

scp，全称<strong style="color:red">s</strong>ecure <strong style="color:red">c</strong>o<strong style="color:red">p</strong>y，用于Linux之间复制文件和目录。

语法：

```shell
scp [options] 源文件路径 目标路径 
```

选项:

* `-r`：递归复制目录下的所有文件，包括目录本身
* `-P port`：指定端口号
* `-i identity_file`：指定私钥文件

示例：

* 从本地上传文件到服务器

将本地的/home/hegongshan/Desktop/robots.txt文件上传到服务器118.190.95.35的/usr/local/tomcat/目录下

```
scp /home/hegongshan/Desktop/xxx.txt root@118.190.95.35:/usr/local/tomcat/
```

* 从服务器下载文件

从118.190.95.35将/usr/local/tomcat/webapps/ROOT.war下载到本机的/home/hegongshan/Desktop/目录下

```shell
scp root@118.190.95.35:/usr/local/tomcat/webapps/ROOT.war /home/hegongshan/Desktop/
```

* 从服务器复制目录（文件夹）

从118.190.95.35将/usr/local/tomcat/webapps/ROOT复制到本机的/home/hegongshan/Desktop/目录下

```shell
scp -r root@118.190.95.35:/usr/local/tomcat/webapps/ROOT /home/hegongshan/Desktop/
```

结果将是在/home/hegongshan/Desktop/下有一个ROOT文件夹。
