经常会遇到，在同一台机器上，装了多个版本的软件，如何管理多个版本呢？

比如，不同的应用可能需要不同版本的GCC。假设本机上存在两个版本的GCC：

```shell
# 4.8.5
/usr/bin/gcc
# 11.2.0
/usr/local/bin/gcc
```

当然，我们可以手动修改路径名。例如现在要使用`v4.8.5`，则对`v11.2.0`执行重命名：

```shell
mv /usr/local/bin/gcc /usr/local/bin/gcc-11.2.0
```

编译完以后，再将名称改回来。

那么，有没有自动化的工具来管理软件的多个版本，在多个版本间进行快速的切换呢？答案是肯定的——update-alternatives！

### 添加alternatives组

```shell
update-alternatives --install <link> <name> <path> <priority>
```

name: 主链接的名称，位于`/etc/alternatives`下

link：主链接的软链接

path：可供主链接选择的链接路径

priority：优先级，默认选择优先级最高的版本

![alternatives结构](/img/alternatives-structure.png)

下面以gcc为例，使用`/usr/bin/gcc`作为各个版本GCC的软链接。

首先，对现有的gcc执行重命名：

```shell
mv /usr/bin/gcc /usr/bin/gcc-4.8.5
mv /usr/local/bin/gcc /usr/local/bin/gcc-11.2.0
```

然后，添加一个新的可选组。

```shell
update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8.5 10
update-alternatives --install /usr/bin/gcc gcc /usr/local/bin/gcc-11.2.0 9
```

验证下：

```shell
[root@hgs ~]# ls -l /usr/bin/gcc
lrwxrwxrwx. 1 root root 21 12月 21 02:50 /usr/bin/gcc -> /etc/alternatives/gcc
[root@hgs ~]# ls -l /etc/alternatives/gcc
lrwxrwxrwx. 1 root root 18 12月 21 02:50 /etc/alternatives/gcc -> /usr/bin/gcc-4.8.5
```

在上面的例子中：

* 主链接：`/etc/alternatives/gcc`

* 主链接的软链接：`/usr/bin/gcc`

* 可供主链接选择的链接路径有`/usr/bin/gcc-4.8.5`和`/usr/local/bin/gcc-11.2.0`

### 查看alternatives组

```shell
update-alternatives --display <name>
```

例如：

```shell
update-alternatives --display gcc
```

### 切换版本

```shell
update-alternatives --config <name>
```

例如：

```shell
update-alternatives --config gcc
update-alternatives --display gcc
```

自动模式，即指向优先级最高的版本。

```shell
update-alternatives --auto <name>
```

### 删除某个版本

如果没有其他版本，则会删除name。

```shell
update-alternatives --remove <name> <path>
```

### 发行版差异

1.命令名

对于CentOS，命令名为`alternatives`，`update-alternatives`是`alternatives`的软链接；

对于Ubuntu，命令名为`update-alternatives`。

2.主链接所在目录：

```bash
/etc/alternatives
```

3.配置文件所在目录：

对于CentOS，位于`/var/lib/alternatives`；

对于Ubuntu，则位于`/var/lib/dpkg/alternatives`。

配置文件记录了每个name对应的link、所有path及其优先级。
