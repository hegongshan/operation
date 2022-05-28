作为Linux三剑客之一，grep（<strong style='color:red'>G</strong>lobally search a <strong style='color:red'>R</strong>egular <strong style='color:red'>E</strong>xpression and <strong style='color:red'>P</strong>rint）是一种强大的文本搜索工具。

选项

* -E：支持正则表达式

* -i：忽略大小写

* -n：输出对应的行号

* -o: 只打印行中匹配的那部分文本

* -r：对子目录进行递归搜索

* -v：打印不匹配的行

* `--color`: 为匹配的文本添加颜色(默认为红色)，有三个可选值：
1.never（不带颜色）
2.always（在任何情况下都带上颜色，在使用管道或重定向时会添加多余的控制字符）
3.auto（只在输出到终端时添加颜色）

在macOS中，`--color`选项的默认值为never。为了使输出的结果带有颜色，可以修改`~/.bash_profile`文件，在其中添加一行：

```shell
alias grep='grep --color=auto'
```

### 实践

1.如果文件test.log有100w行，查找含有“error”的行并显示对应的行号。（2020年4月8日，腾讯一面）

```shell
grep -n "error" test.log
```

2.[LeetCode 193. 有效电话号码](https://leetcode.cn/problems/valid-phone-numbers/)

```bash
grep -E "^(\([0-9]{3}\) |[0-9]{3}-)[0-9]{3}-[0-9]{4}$" file.txt
```

