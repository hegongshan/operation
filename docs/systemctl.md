---
title: 在Linux中存活下来之服务管理systemctl
date: 2021-11-15 16:03:15
tags:
---



### 服务

```shell
systemctl start sshd
systemctl stop sshd
systemctl status sshd
systemctl restart sshd
```

### 设置/禁止开机自启动

```shell
systemctl enable sshd

systemctl disable sshd
```

