CentOS使用的包管理器是YUM；而Ubuntu使用的则是APT。

### 安装软件

```bash
apt install <package>
```

### 列出软件

* 列出安装的包

```bash
apt list --installed
```

注意：`yum`在列出已安装的包时，`installed`没有前缀`--`；`apt`则有前缀`--installed`

* 列出可升级的包

```bash
apt list --upgradeable
```

* 列出所有可用的包

```bash
apt list --all-versions
```

### 查看包的相关信息

```bash
apt info <package>
```

