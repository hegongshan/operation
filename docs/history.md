history命令用于查看历史执行过的命令。

### 命令描述

选项

* -c：清空历史列表
* -d offset：删除历史列表中第offset个命令
* -w: 将当前历史命令写入历史文件中

参数

* n：查看最近的n条命令

### 相关变量

1.HISTSIZE：history命令显示的命令条数，默认值为1000。

2.HISTFILE：历史命令的存储文件，默认值为~/.bash_history。

~/.bash_history存储的是当前登录之前执行过的历史命令，本次登录以后执行的命令暂时存储在内存中，使用history命令即可查看。默认情况下，退出账号后，暂存在内存中的历史命令才会追加到存储文件中。

3.HISTFILESIZE：文件中存储的命令条数，默认值也为1000。

4.如果需要修改上述变量的默认值，可以在~/.bash_profile中设置变量值。

例如，将存储文件设置为/root/history.conf，HISTSIZE设置为1500：

首先，在~/.bash_profile添加如下内容

```sh
HISTFILE=/root/history.conf
HISTSIZE=1500
```

然后，执行如下命令使上述设置生效

```shell
source ~/.bash_profile
```

最后，执行如下命令，查看设置是否成功

```shell
echo $HISTFILE $HISTSIZE
```

### 执行历史命令

1.使用!number执行第number条命令

2.使用!!执行上一条命令
