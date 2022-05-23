at也可以用于定时任务，其只执行一次。

### 安装at

安装at

```shell
yum install -y at
```

启动守护进程

```shell
systemctl start atd
```

### 添加任务

```shell
at -f <file> <time>
```

