# getopts

### 语法说明
```bash
getopts optstring name
```

* `optstring`：包含需要识别的选项字符。

如果选项字符后面有冒号，说明该选项需要一个参数，选项和参数之间使用空格分隔。

* `name`：下一个选项。

在getopts中，还包含几个Shell变量：

* `OPTIND`：下一个选项的索引

* `OPTARG`：当选项需要参数时，包含参数值

示例：

```bash
$ cat test.sh
#!/bin/bash
while getopts hd: name; do
    case $name in
    h)
        echo "help"
        ;;
    d)
        echo "-d $OPTARG"
        ;;
    :)
        echo "slient mode: $OPTARG"
        ;;
    ?)
        echo "unknown: $OPTARG"
        ;;
    esac
done
```

执行结果如下所示：

```bash
$ ./test.sh -h -d 1
help
-d 1
```

### 错误处理

1.在getops中，若不想输出错误信息，有以下两种方法：

* 如果`optstring`的第一个字符为冒号，getopts将进入<strong style="color:red;">沉默模式</strong>，此时不会输出任何错误信息；

* 设置Shell变量`OPTERR`的值：如果为0，即使`optstring`的第一个字符不是冒号，也不会输出错误信息。默认为1。

2.若发现无效选项，getopts会将`name`赋值为`?`

* 当前为沉默模式，将`OPTARG`赋值为发现的选项字符；

```bash
# 修改test.sh，为选项字符串添加前导:
while getopts :hd: name; do
    # 省略了中间的内容
done
```

执行结果如下所示：

```bash
$ ./test.sh -x 
unknown: x
```

* 当前不是沉默模式，打印错误信息，并删除变量`OPTARG`；

```bash
$ ./test.sh -x
./test.sh: illegal option -- x
unknown: 
```

3.若需要的参数未被设置

* 当前为沉默模式，getopts会将`name`赋值为`:`，同时将`OPTARG`赋值为选项字符。

```bash
$ ./test.sh -d
slient mode: d
```

* 当前不是沉默模式，getopts会将`name`赋值为`?`，打印错误信息，并删除变量`OPTARG`。

```bash
$ ./test.sh -d
./test.sh: option requires an argument -- d
unknown: 
```

