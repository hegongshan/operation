---
title: 在Linux中存活下来之时间管理工具timedatectl
date: 2022-02-17 15:58:12
tags: linux
categories: linux
---

本文介绍了时间管理工具timedatectl。

time：时间，x时x分x秒
date：日期，x年x月x日

<!--more-->

1.查看当前时间设置

```bash
timedatectl status
```

输出结果如下：

```bash
$ timedatectl status
      Local time: 四 2022-02-17 03:03:22 EST
  Universal time: 四 2022-02-17 08:03:22 UTC
        RTC time: 四 2022-02-17 08:03:23
       Time zone: America/New_York (EST, -0500)
     NTP enabled: yes
NTP synchronized: no
 RTC in local TZ: no
      DST active: no
 Last DST change: DST ended at
                  日 2021-11-07 01:59:59 EDT
                  日 2021-11-07 01:00:00 EST
 Next DST change: DST begins (the clock jumps one hour forward) at
                  日 2022-03-13 01:59:59 EST
                  日 2022-03-13 03:00:00 EDT
```

从上述结果可以看出，本机使用的是纽约时间。

2.设置当前时间

```bash
timedatectl set-time TIME
```

3.设置时区

```bash
timedatectl set-timezone ZONE
timedatectl list-timezones
```

将本机时区修改为上海时间。

```bash
$ timedatectl list-timezones | grep -i shanghai
Asia/Shanghai
$ timedatectl set-timezone Asia/Shanghai
$ timedatectl status
      Local time: 四 2022-02-17 16:10:43 CST
  Universal time: 四 2022-02-17 08:10:43 UTC
        RTC time: 四 2022-02-17 08:10:44
       Time zone: Asia/Shanghai (CST, +0800)
     NTP enabled: yes
NTP synchronized: no
 RTC in local TZ: no
      DST active: n/a
```
