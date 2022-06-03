Shell脚本是一门比较简单的语言，其难点在于：第一，需要熟悉Linux的相关命令；第二，与众不同的独特语法。

习惯了使用高级语言进行编程，切换到Shell编程，可能会不太自然。

本文总结了Shell编程中与其他高级语言的不同之处。

```shell
Shell脚本
	|
Shell解释器
	|
C语言
```

### 指定解释器

在`*.sh`第一行，需要指定shell脚本的解释器，通常使用`bash`：

```shell
#!/bin/bash
```

### 变量

#### 定义变量

变量名和等号两边不能有空格：

```bash
name=“hello”
```

#### 引用变量

使用`$变量名`或者`${变量名}`：

```bash
echo $name ${name}
```

#### 设置默认值

使用`${变量名:-默认值}`可以为变量设置默认值：

```bash
echo ${name:-me}
```

#### 局部变量

默认情况下，Shell中定义的变量均为全局变量。如果要定义局部变量，则需要使用`local`来修饰：

```bash
local name="me"
```

### 字符串

* 单引号中不能使用变量，双引号中可以使用变量。

```shell
$ echo '$PATH'
$PATH
$ echo "$PATH"
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

### 语句分隔

默认情况下，一行就是一条语句，不需要使用分号`;`作为结束符，这和Python是相似的。

如果需要在一行中输入多条语句，可以使用`;`、`||`、`&&`分隔。

```bash
# 后一条语句在前一条语句执行失败之后才执行
true || echo "Hello"

# 后一条语句在前一条语句执行成功之后才执行
make -j8 && make install

# 前后的语句没有关系
echo "Hello" ; echo " world\n"
```

### 获取命令的执行结果

1.使用反引号

```bash
res=`ls -l | grep yml`
echo $res
```

2.使用`$(命令)`

```bash
res=$(ls -l | grep yml)
echo $res
```

### 算术运算

* 整数运算。在Shell脚本中，整数运算可以使用`expr`命令或者美元符+双括号`$(())`两种方法。

```bash
expr 1 + 2
echo $((1 + 2))

expr 1 \* 2
echo $((1 * 2))
```

值得注意的是，在双括号`$(())`中，引用变量不需要使用美元符`$`。

* 浮点数。Shell只支持整数运算，不支持浮点数运算。

如果要进行浮点数运算，则需要使用浮点数计算工具bc（全称为Basic Calculator）。

```shell
# CentOS
yum install -y bc
# Ubuntu
apt install -y bc
```

例如：

```bash
echo "1.5 + 2.3" | bc
```

### 条件判断

#### 写法

* `if...then`占两行的写法

```bash
if []
then
	...
fi
```

* `if...then`占一行的写法：用分号`;`分隔`]`和`then`

```bash
if []; then
	...
fi
```

#### 条件表达式

在Shell脚本中，条件表达式一般写在中括号`[]`中（test命令与中括号是等价的）。

* 关系运算符（只支持数字）

在Shell中，`>`和`<`有特殊的含义，无法直接用于表示大于或小于等关系运算。

需要使用如下的字母形式来表示关系运算：

```bash
-lt（less than）
-gt（greater than）
-eq（equal）
-ne（not equal）
-le（less than or equal）
-ge (greater than or equal)
```

* 逻辑运算符

使用单个中括号时，必须使用`-a`表示逻辑与，`-o`表示逻辑或；

使用两个中括号（逻辑扩展）时，必须使用`&&`表示逻辑与，`||`表示逻辑或；

单个中括号和两个中括号均使用`!`表示逻辑非。

```bash
if [ 200 -gt 100 -a 2 -gt 1 ]; then
	...
fi

if [[ 200 -gt 100 && 2 -gt 1 ]]; then
	...
fi

if [[ ! 200 -gt 100 && 2 -gt 1 ]]; then
	...
fi
```

注意：中括号左右必须有空格。

* 字符串运算符

```bash
-z string # zero，判断字符串长度是否为0
-n string # 判断字符串长度是否不为0
```

* 文件测试运算符

```bash
# 判断文件类型
-f file 是否为普通文件
-d file 是否为目录

-e file 是否存在

# 判断文件模式
-r file
-w file
-x file
```

### 循环

#### for循环

1.原生的for循环

```bash
for var in item1 item2 ... itemN
do
	...
done

for var in item1 item2 ... itemN; do
	...
done

for var in item1 item2 ... itemN; do ... done;
```

2.C语言风格的for循环：使用双括号`(())`

```bash
for ((i = 0; i < 10; i++)); do
	...
done
```

### 函数调用

1.函数定义

```bash
[ function ] function_name [()] {

}
```

2.传递参数

在其他的高级语言中，通常需要指定入参的名字，以便在函数内部引用变量

```shell
function_name(arg1, arg2) {

}
```

然而，Shell脚本没有这个操作，函数定义的`()`是空的，不用指定参数的名字。

在函数内部使用`$n`来引用传入的参数，例如，`$1`表示第一个参数，`$2`表示第二个参数：

```bash
hello_world() {
    echo "$1 $2"
}
```

调用时，不要写括号，参数跟在函数名后面，用空格进行分隔：

```bash
# C语言：hello_world(2)
hello_world 2 3
```

### 文件包含

与C语言中的`#include`、Java和Python中的`import`类似，Shell中也可以包含外部脚本。

在Shell脚本中，文件包含的语法格式如下：

```bash
source bashrc

或者

. bashrc # 点号(.)和文件名中间有空格
```

### 进程同步

```shell
wait [n]
```

其中，n可以是进程的ID号，也可以是作业的ID号。

下面是一种常见的用法：

```bash
wait $!
```

其中，`$!`表示后台运行的最后一个进程的ID号。

