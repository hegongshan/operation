# 花括号扩展（Brace Expansion）

### 查看手册

```bash
man bash
```

搜索`Brace Expansion`说明内容

```bash
/Brace Expansion
```

### 使用说明

花括号扩展不能被单引号或者双引号包裹，它有以下两种使用形式：

1.一对花括号之间是一系列逗号分隔的字符串`{x,y,z}`，逗号左右不能有空格。

![](../img/bash-brace-expansion-comma-separated-strings.png)

其中，前缀和后缀是可选的。

示例：

```bash
$ echo a{d,c,b}e
ade ace abe
```

2.一对花括号之间是一个序列表达式`{x..y}`，`..`左右不能有空格。

![](../img/bash-brace-expansion-sequence.png)

其中，

* x和y要么是整数，要么是单个字符，二者必须是相同类型的；
* 左右两边都是闭区间，即`[x, y]`；
* 前缀和后缀是可选的。

示例：

```bash
$ echo {1..10}
1 2 3 4 5 6 7 8 9 10
$ echo a{b..d}e
abe ace ade
```

