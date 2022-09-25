在Linux中，查看文件内容的常用命令有head、tail、cat、tac、more以及less。

### head

head -- display first lines of a file

```sh
head [-n count | -c bytes] [file ...]
```

* -n：显示文件的前n行。n默认为10。
* -c：显示文件的前c个字节。n默认为为10。

不带参数的head等价于`head -n 10`。

如果指定了多个文件，则每个文件前面都有一个由字符串“ ==> XXX <== ”组成的标头，其中XXX是文件名称。

### tail

tail -- display the last part of a file

```sh
tail [-F | -f | -r] [-q] [-b number | -c number | -n number] [file ...]
```

* -b：显示文件的后number个512字节块。
* -c：显示文件的后number个字节。
* -f：循环读取
* -n：显示文件的后number行
* -q：不显示文件名称。
* -r：按照从后往前的顺序输出。

**如果number前面有+号，表示从第number开始到文件末尾。**

如果指定了多个文件，则每个文件前面都有一个由字符串“ ==> XXX <== ”组成的标头，其中XXX是文件名称。

如果指定了-q参数，则不会输出由字符串“ ==> XXX <== ”组成的标头。

示例：

1.显示err.log的最后20行

```shell
tail -n 20 err.log
```

2.显示err.log的内容，从第20行至文件末尾

```shell
tail -n +20 err.log
```

### cat

拼接文件并打印到屏幕上。

选项

* -n：显示行号

### tac

与cat相比，tac按照相反的顺序打印文件内容。

### more/less

more只能向前移动↓。

与more相比，less支持向前移动↓和向后移动↑两种查看方式。

空格键：查看下一屏

B键：查看上一屏

Q键：退出

* 搜索

/pattern：从当前位置向前搜索↓包含pattern的内容

?pattern：从当前位置向后搜索↑包含pattern的内容

n键：跳转到下一个匹配

N键：跳转到上一个匹配
