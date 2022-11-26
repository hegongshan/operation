经常会遇到，在同一台机器上，装了多个版本的软件，如何管理多个版本呢？

比如，不同的应用可能需要不同版本的GCC。假设本机上存在两个版本的GCC：

```bash
# 4.8.5
/usr/bin/gcc
# 11.2.0
/usr/local/bin/gcc
```

当然，我们可以手动修改路径名。例如现在要使用`v4.8.5`，则对`v11.2.0`执行重命名：

```bash
mv /usr/local/bin/gcc /usr/local/bin/gcc-11.2.0
```

编译完以后，再将名称改回来。

那么，有没有自动化的工具来管理软件的多个版本，在多个版本间进行快速的切换呢？答案是肯定的——update-alternatives！

> 对于CentOS，命令名为`alternatives`，`update-alternatives`是`alternatives`的软链接；
>
> 对于Ubuntu，命令名为`update-alternatives`。

### 添加alternatives组

```bash
update-alternatives --install <link> <name> <path> <priority>
```

* name: 主链接的名称，位于`/etc/alternatives`下

* link：主链接的软链接

* path：可供主链接选择的链接路径

* priority：优先级，默认选择优先级最高的版本

![alternatives结构](/img/alternatives-structure.png)

以CentOS为例，上述命令将会执行以下操作：

* 在`/var/lib/alternatives`目录下生成名为`name`的文件，记录`link`、`path`以及`priority`。（对于Ubuntu，目录名为`/var/lib/dpkg/alternatives`）

* 在`/etc/alternatives`目录下创建软链接`name`，指向优先级最高的路径
* 创建软链接`link`，指向文件`/etc/alternatives/${name}`

实例：

下面以GCC为例，使用`/usr/bin/gcc`作为各个版本GCC的软链接。

首先，对现有的GCC执行重命名：

```bash
mv /usr/bin/gcc /usr/bin/gcc-4.8.5
mv /usr/local/bin/gcc /usr/local/bin/gcc-11.2.0
```

然后，添加一个新的可选组。

```bash
update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8.5 10
update-alternatives --install /usr/bin/gcc gcc /usr/local/bin/gcc-11.2.0 9
```

接着，验证下软链接：

```bash
[root@hgs ~]# ls -l /usr/bin/gcc
lrwxrwxrwx. 1 root root 21 12月 21 02:50 /usr/bin/gcc -> /etc/alternatives/gcc
[root@hgs ~]# ls -l /etc/alternatives/gcc
lrwxrwxrwx. 1 root root 18 12月 21 02:50 /etc/alternatives/gcc -> /usr/bin/gcc-4.8.5
```

在上面的例子中：

* 主链接：`/etc/alternatives/gcc`
* 主链接的软链接：`/usr/bin/gcc`
* 可供主链接选择的链接路径有`/usr/bin/gcc-4.8.5`和`/usr/local/bin/gcc-11.2.0`

最后，检查下配置信息

```bash
[root@hgs ~]# cat /var/lib/alternatives/gcc
auto
/usr/bin/gcc

/usr/bin/gcc-4.8.5
10
/usr/local/bin/gcc-11.2.0
9
```

其中，第一行表示当前的模式（关于模式的使用参看[切换版本](#切换版本)）：

* `auto`表示自动模式，name自动指向优先级最高的路径；
* `manual`表示手动模式，用户手动设置了name指向的路径。

### 查看alternatives组

1.查看某个组

```bash
update-alternatives --display <name>
```

例如：

```bash
[root@hgs ~]# update-alternatives --display gcc
gcc - 状态为自动。
链接当前指向 /usr/bin/gcc-4.8.5
/usr/bin/gcc-4.8.5 - priority 10
/usr/local/bin/gcc-11.2.0 - priority 9
当前“最佳”版本是 /usr/bin/gcc-4.8.5。
```

2.查看所有组

```bash
update-alternatives --list
```

### 切换版本

* 交互式

1.手动模式

```bash
update-alternatives --config <name>
```

该方式会列出所有可供选择的路径，例如：

```bash
[root@hgs ~]# update-alternatives --config gcc

共有 2 个提供“gcc”的程序。

  选项    命令
-----------------------------------------------
*+ 1           /usr/bin/gcc-4.8.5
   2           /usr/local/bin/gcc-11.2.0

按 Enter 保留当前选项[+]，或者键入选项编号：2
```

检查切换：

```bash
[root@hgs ~]# update-alternatives --display gcc
gcc - 状态为手工。
链接当前指向 /usr/local/bin/gcc-11.2.0
/usr/bin/gcc-4.8.5 - priority 10
/usr/local/bin/gcc-11.2.0 - priority 9
当前“最佳”版本是 /usr/bin/gcc-4.8.5
```

2.自动模式，指向优先级最高的版本。

```bash
update-alternatives --auto <name>
```

例如：

```bash
[root@hgs ~]# update-alternatives --auto gcc
[root@hgs ~]# update-alternatives --display gcc
gcc - 状态为自动。
链接当前指向 /usr/bin/gcc-4.8.5
/usr/bin/gcc-4.8.5 - priority 10
/usr/local/bin/gcc-11.2.0 - priority 9
当前“最佳”版本是 /usr/bin/gcc-4.8.5。
```

* 非交互式

```bash
update-alternatives --set <name> <path>
```

示例：

```bash
[root@hgs ~]# update-alternatives --set gcc /usr/local/bin/gcc-11.2.0
[root@hgs ~]# update-alternatives --display gcc
gcc - 状态为手工。
链接当前指向 /usr/local/bin/gcc-11.2.0
/usr/bin/gcc-4.8.5 - priority 10
/usr/local/bin/gcc-11.2.0 - priority 9
当前“最佳”版本是 /usr/bin/gcc-4.8.5。
```

### 删除某个版本

```bash
update-alternatives --remove <name> <path>
```

若删除path后，name已经没有其他版本，则会删除`/etc/alternatives/<name>`和`<link>`。
