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

### sftp

sftp全称为Secure File Transfer Protocol，即安全的文件传输协议。

#### 工作原理

流程图

#### 上手实践

使用sftp协议登录ftp服务器：

```bash
sftp user@ip
```

与scp相比，sftp可以方便的操作本地和远程目录。

1.下载

```bash
get [-afPpRr] remote [local]
```

2.上传

```bash
put local [remote]
```

3.目录操作

```bash
cd
rm

lcd == !cd
lrm == !rm
```

lcommand  == !command，表示在本地执行command命令。

其中，l为local的首字母缩写。

4.退出

```bash
bye
quit
exit
```

5.查看帮助信息

```bash
help
?
```
