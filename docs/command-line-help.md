本文对Linux中的各类帮助命令进行了总结，如man和help等。

### Linux命令分类

Linux命令可以分为两类：内部命令（Internal Commands, Shell Built-in Commands）和外部命令（External Commands）。

|   类型   | 说明                                                  | 是否需要从环境变量PATH中搜索命令所在的路径 |         是否需要创建进程去执行         |
| :------: | ----------------------------------------------------- | :----------------------------------------: | :------------------------------------: |
| 内部命令 | Shell中的内置命令，例如，cd                           |    <strong style="color:red">✘</strong>    |  <strong style="color:red">✘</strong>  |
| 外部命令 | 可执行文件，通常位于`/bin`、`/usr/bin`，例如，ls和cat |   <strong style="color:green">✔︎</strong>   | <strong style="color:green">✔︎</strong> |

### 查看外部命令

#### man

#### apropos

#### whatis

搜索whatis数据库


查看命令的帮助手册

#### info

查看信息文档

### 查看内置命令

* 查看Shell中的所有内置命令

```shell
man builtin
```

* 如果要查看Shell内置命令的帮助信息，则需要使用`help`命令。

例如，history是Shell的内置命令，

```
$ help history
```

### 查看命令的类型

type是一个Shell内置命令，用于查看命令的类型。

```shell
type name [name ...]
```

* 查看内置命令

```shell
hegongshan@hgs:~/Desktop$ type type history hash
type is a shell builtin
history is a shell builtin
hash is a shell builtin
```

①`xxx is a shell builtin`表明其是一个Shell内置命令。

* 查看外部命令

```shell
hegongshan@hgs:~/Desktop$ type cat ls
cat is /usr/bin/cat
ls is aliased to `ls --color=auto'
```

②`xxx is path`表明xxx的路径为path；

③`xxx is aliased to command `表明xxx是命令command的别名。

```shell
hegongshan@hgs:~/Desktop$ echo "hello" > hello.txt
hegongshan@hgs:~/Desktop$ cat hello.txt 
hello
hegongshan@hgs:~/Desktop$ type cat
cat is hashed (/usr/bin/cat)
```

④`xxx is hashed (path)`表明xxx的执行路径已经被缓存在哈希表中。当再次执行xxx时，不需要再从环境变量PATH中寻找xxx的执行路径。

```shell
hegongshan@hgs:~/Desktop$ hash -l
builtin hash -p /usr/bin/cat cat
# 删除某项
hegongshan@hgs:~/Desktop$ hash -d cat

# 清空整个哈希表
hegongshan@hgs:~/Desktop$ hash -r
hegongshan@hgs:~/Desktop$ hash -l
hash: hash table empty

# 添加某项
hegongshan@hgs:~/Desktop$ hash -p /usr/bin/cat cat
hegongshan@hgs:~/Desktop$ hash -l
builtin hash -p /usr/bin/cat cat
```

### 查看命令的位置

which

```shell
hegongshan@hgs:~/Desktop$ which cat
/usr/bin/cat

hegongshan@hgs:~/Desktop$ which ls
/usr/bin/ls
```

