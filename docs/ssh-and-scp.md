前面我们讲了如何在Windows系统中登录Linux服务器，以及实现windows和Linux之间的文件传输操作。今天我们来讲下在Linux系统（如ubuntu）中如何登录Linux服务器及实现文件传输。

Linux中使用**ssh命令**登录其他的Linux，使用**scp命令**实现文件传输。

<!--more-->

### ssh

ssh，全称Secure Shell，是一种用于远程登录的协议。

语法：

```shell
ssh 用户名@IP地址
```

示例：

这里以root用户和 IP 地址118.190.95.35（从网上随便找的一个IP）为例

```shell
ssh root@118.190.95.35
```

### scp

scp，全称Secure Copy，用于Linux之间复制文件和目录。

语法：

```shell
scp [options] 源文件路径 目标路径 
```

参数:

* `-r`：递归复制目录下的所有文件，包括目录本身
* `-P port`：指定端口号

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
