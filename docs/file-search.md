### locate

安装locate工具

```shell
yum install -y mlocate
```

首次执行时，会报如下的错误：

```shell
locate: 无法执行 stat () `/var/lib/mlocate/mlocate.db': 没有那个文件或目录
```

此时，需要生成下数据库：

```shell
updatedb
```

然后，就可以去查找文件：

```shell
locate xxx
```

### find

```shell
find [-L] <dir> -name <name>
```

示例：2022年11月5日，信息安全工程师试题

```bash
$ echo "Hello world" > hello.txt
$ ln -s hello.txt hello_symlink.txt
```

* 查看失效的符号链接

```bash
$ find -L /home -type l
```

* 删除失效的符号链接

```bash
$ find -L /home -type l -exec rm -f {} +;
```
