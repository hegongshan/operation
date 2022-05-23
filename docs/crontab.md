crontab共有两种用法：

```shell
crontab [-u user] file
crontab [-u user] { -l | -r | -e }
```

### 添加定时任务

#### 通过命令行添加定时任务

执行文字编辑器来设定时程表。默认的编辑器为vi。

```shell
crontab -e
```

时程表中的每一行代表一个定时任务，其格式如下：

```shell
minute hour dayOfMonth month dayOfWeek command
```

minute的取值范围为0~59，

hour的取值范围为0~11

dayOfMonth（一个月中的第几天）的取值范围为1~31

month的取值范围为1~12

dayOfWeek（一周中的星期几）的取值范围为0~6（0表示星期天）

特殊的表示：

* `*`表示所有可能的值

```shell
* * * * * ls
```

* `a,b,c`表示取值为{a,b,c}

例如，在每天的22时0分和23时0分执行一次

```shell
0 22,23 * * * ls
```

* `/n`表示时间间隔为n

例如，在每年12月，从0点到23点，每隔2个小时0分钟执行一次ls。

```shell
0 */2 * 12 * ls
```

* `a-b`表示取值范围为$[a, b]$

```shell
1-10 * * * * ls
```

#### 使用文件添加定时任务

```shell
crontab [-u user] file
```

首先，新建任务文件tab，内容如下：

```shell
* * * * * ~/Desktop/test.sh
```

表示每秒执行一次脚本`~/Desktop/test.sh`

然后，添加任务：

```shell
crontab tab
```

### 查看定时任务

```shell
crontab -l
```

### 删除定时任务

1.打开时程表删除某一个任务

```shell
crontab -e
```

找到需要删除的任务，删除并保存。

2.清空时程表

```shell
crontab -r
```

