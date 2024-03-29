> 前话：学习Vim编辑器，是一个循序渐进的过程，本篇是博主自己的学习总结，会持续更新。

### 简介

Vim编辑器有三种工作模式：

* 命令行模式：顾名思义，在这个模式下，所有的键盘操作都会被认为是命令。启动vim编辑器，就会进入命令行模式。
* 输入模式：除了按下“Esc”外，其他的键盘输入都不会被认为是命令。处于这个模式下，和我们在Windows中用Notepad等编辑文件，几乎没有区别。按下“Esc"，会退出输入模式，进入命令行模式。
* 末行模式（编辑模式）：在命令模式下，输入“:”就会进入末行模式。

这里，博主总结下最近学习到的且经常使用的一些命令。

<!--more-->

### 启动Vim

vim fileName：进入编辑环境并打开或新建文件

### 命令行模式

#### 编辑

dd：删除光标所在行，并将当前行内容复制到剪贴板

p（小写）：全称paste，表示将剪贴板中的数据粘贴到光标下一行

P（大写）：将剪贴板中的数据粘贴到光标上一行

yy：复制光标所在行

nyy：复制从光标所在行开始向下数n行

#### 移动光标

^：移至行首

$：移至行尾

### 进入输入模式

* i：在命令模式下，在当前光标处进入输入模式

### 输入模式

输入模式，类似于我们在Windows中编辑文件

* 方向键进行上下左右方向的光标移动
* Backspace键：删除光标左侧的字符
* delete键：删除光标右侧的字符

### 退出输入模式

按下Esc键：从输入模式回到命令行模式

### 进入末行模式

在命令行模式下，按下`:`就会进入末行模式。

输入`:set number`或者`:set nu`显示行号。

输入`:set nonumber`或者`:set nonu`不显示行号。

输入`:set list`，可以显示空白字符（如换行和缩进等）

清空文件：`:%d`

### 退出Vim

q：退出Vim

q!：不保存文件并退出Vim

w：保存文件

wq：保存文件并退出Vim

wq!：强制保存文件并退出vi（忽略只读）

### 快速定位行

1.启动前

定位到文件第num行：vim +num fileName

例如，定位到test.txt的第10行：vim +10 test.txt

2.命令行模式

`gg`：跳转至第一行

`G`：跳转至最后一行

`nG` 或者 `ngg`：跳转至第n行。比如10G/10gg，表示跳转至第10行

3.末行模式

输入`:number`，定位到第number行。

