---
title: sftp协议
date: 2022-02-23 21:46:31
tags: linux
Categories: linux
---

sftp全称为Secure File Transfer Protocol，即安全的文件传输协议。

<!--more-->

### 工作原理

流程图

### 上手实践

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

