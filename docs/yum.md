YUM（Yellowdog Updater Modified）是Linux中的一个软件包管理器。

常用选项：

```shell
# 是否继续？[y/N]：
-y, --assumeyes
```

所有的询问都回答yes。

### 搜索包

```shell
yum search package1 [package2] [...]
```

查看包的所有版本

```shell
yum search --showduplicates package
```

### 查看包信息

```shell
yum info package1 [package2] [...]
```

### 查看包依赖

```shell
yum deplist package1 [package2] [...]
```

### 安装包

```shell
yum install -y package1 [package2] [...]
```

安装指定版本的包：

```shell
yum install -y package=version
```

### 更新包

1.检查更新

```shell
yum check-update
```

2.更新所有已安装的包

```shell
yum update
```

3.更新指定的包

```shell
yum update package1 [package2] [...]
```

### 删除包

```shell
yum remove package1 [package2] [...]
```

### 查看包列表

1.查看已安装的包

```shell
yum list installed
```

2.查看可以安装的包

```shell
yum list available
```

3.查看所有已安装+可以安装的包

```shell
yum list
```

### 查看命令所在的包

```bash
yum provides 命令
```
