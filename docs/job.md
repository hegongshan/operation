---
title: 在Linux中存活下来之作业管理
date: 2021-09-17 11:55:17
tags: linux
categories: linux
---

作业管理

<!--more-->

### jobs

查看当前Shell中的作业信息。

```shell
jobs: usage: jobs [-lnprs] [jobspec ...] or jobs -x command [args]
```

* -l：在原有信息的基础上，额外显示作业的PID

* -p：只输出作业的PID
* -r：只输出运行（running）状态的作业
* -s：只输出停止（stopped）状态的作业

### bg

bg，全称background，用于让前台作业在后台运行。

```shell
bg: usage: bg [job_spec ...]
```

### fg

fg，全称foreground，用于让后台作业在前台运行或者让暂停的前台作业继续运行。

```shell
fg: usage: fg [job_spec]
```

### 示例

* 新建test.sh，内容如下：

```shell
#!/bin/bash

while true; do
	echo 1 > /dev/null
done
```

* 添加执行权限并运行

```shell
hgs:Desktop hegongshan$ chmod +x test.sh 
hgs:Desktop hegongshan$ ./test.sh &
[1] 16005
```

输出中[1]表示作业号为1，进程号（PID）为16005。

* 查看作业

```shell
hgs:Desktop hegongshan$ jobs
[1]+  Running                 ./test.sh &
```

* 让作业在前台运行

```shell
hgs:Desktop hegongshan$ fg %1
./test.sh

```


* 暂停作业：按下`Ctrl`+`Z`可以暂停作业

```shell
hgs:Desktop hegongshan$ fg %1
./test.sh
^Z
[1]+  Stopped                 ./test.sh
```


* 让作业继续在后台运行

```shell
hgs:Desktop hegongshan$ bg %1
[1]+ ./test.sh &
```


* 结束作业：强制结束，使用kill %作业号

```shell
hgs:Desktop hegongshan$ kill -9 %1
[1]+  Killed: 9               ./test.sh
```
