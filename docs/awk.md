awk是一种强大的文本处理语言，其名字取自三个创始人Alfred **A**ho，Peter **W**einberger和 Brian **K**ernighan的姓氏首字母。

```bash
awk [ -F fs ] [ -v var=value ] [ 'prog' | -f progfile ] [ file ...  ]
```

* -F、--field-separator：指定行中的分隔符，`fs`是一个正则表达式

例如，按照逗号进行分隔：

```bash
awk -F "," '{ print $0 }'
awk -F "[,=|]" '{ print $0 }'
```

prog的格式为：

```shell
pattern {action}
```
如果没有指定pattern，则匹配所有行，即对所有行执行action；如果没有指定action，则打印整行。

在AWK中，有两个特殊的`pattern`——`BEGIN`和`END`：

①`BEGIN`指定的action在读取第一行之前执行；

②`END`指定的action在读取最后一行之后执行。

因此，一个常见的awk模板为
```bash
awk 'BEGIN { } { } END { }' file
```

例如，对于`/etc/passwd`，按照冒号进行分隔，只输出root的信息：

```shell
$ awk -F: '$1 == "root" { print $0 }' /etc/passwd
root:x:0:0:root:/root:/bin/bash
$ awk -F: '{ if ($1 == "root")  print $0 }' /etc/passwd 
root:x:0:0:root:/root:/bin/bash
```

### 变量

`NF`表示字段的个数，`$NF`表示第`NF`个字段的值，即最后一个字段的值。

$(NF - 1)表示倒数第二个字段。

```bash
$ echo "Hello AWK" > test.txt
$ awk '{print $1, $2, $NF, $(NF - 1)}' test.txt
Hello AWK AWK Hello
```

### 函数

* length()：字符串、数组的长度。若没有设置参数，则表示计算当前行`$0`的长度。

```bash
$ awk '{print length, length($1), length($2)}' test.txt 
9 5 3
```

* substr(s, m [, n]])：从字符串s的第m位开始，截取长度为n的子串。如果n没有设置，则表示从m开始到s的末尾。

字符串→整数

整数→字符串

* asort(s [, d [, how] ])：根据值对源数组s进行排序（默认为升序），并用从1开始的整数替换原来的索引，返回s中的元素个数。如果指定了目的数组d，则保持源数组s的索引不变，d存放排序后的值。

how的有效值如下：

| 排序顺序      | 描述                     | 排序顺序       | 描述                     |
| :------------ | :----------------------- | -------------- | ------------------------ |
| @val_str_asc  | 对值按照字符串升序排列   | @val_num_asc   | 对值按照整数升序排列     |
| @val_str_desc | 对值按照字符串降序排列   | @val_num_desc  | 对值按照整数降序排列     |
| @val_type_asc | 对值按照类型进行升序排列 | @val_type_desc | 对值按照类型进行降序排列 |

示例：

```bash
$ cat > test.txt << EOF
https://www.zhihu.com
https://www.baidu.com
https://www.zhihu.com/creator
EOF
$ awk -F "/+" '{
	arr[$2]++
}
END {
	len = asort(arr, d, "@val_num_desc")
  for (i = 1; i <= len; i++) {
  	print d[i], arr[d[i]]
  }
}' test.txt
2 
1
```

* asorti(s [, d [, how] ])：根据索引对源数组s进行排序，值并不会被排序。如果设置了d，则保持源数组s的索引不变，d存放排序后的索引。

how的有效值如下：

| 排序顺序      | 描述                     | 排序顺序       | 描述                     |
| :------------ | :----------------------- | -------------- | ------------------------ |
| @ind_str_asc  | 对索引按照字符串升序排列 | @ind_num_asc   | 对索引按照整数升序排列   |
| @ind_str_desc | 对索引按照字符串降序排列 | @ind_num_desc  | 对索引按照整数降序排列   |

```bash
$ awk -F "/+" '{ arr[$2]++ } END { len = asorti(arr, d); for (i = 1; i <= len; i++) { print d[i], arr[d[i]] } }' test.txt
www.baidu.com 1
www.zhihu.com 2
$ awk -F "/+" '{ arr[$2]++ } END { len = asorti(arr, d, "@ind_num_desc"); for (i = 1; i <= len; i++) { print d[i], arr[d[i]] } }' test.txt
www.zhihu.com 2
www.baidu.com 1
```

### 综合应用

来看下[LeetCode 194.转置文件](https://leetcode-cn.com/problems/transpose-file/):

方法一：取巧——字符串拼接

```bash
awk '{
    for (i = 1; i <= NF; i++) {
        if (NR == 1) {
            res[i-1] = $i;
        } else {
            res[i-1] = res[i-1] " " $i
        }
    }
}
END {
    for (i = 0; i < NF; i++) {
        print res[i]
    } 
}' file.txt
```

方法二：二维数组转置

```bash
awk '{
    for (i = 1; i <= NF; i++) {
        if (NR == 1) {
            res[i-1,0] = $i;
        } else {
            res[i-1,NR-1] = $i
        }
    }
}
END {
    for (i = 0; i < NF; i++) {
        for (j = 0; j < NR; j++) {
            if (j == 0) {
                printf "%s", res[i,j]
            } else {
                printf " %s", res[i,j]
            }
        }
        printf "\n"
    }
}' file.txt
```

### 参考资料

1.The AWK Programming Language

中文翻译：AWK程序设计语言，https://github.com/wuzhouhui/awk

