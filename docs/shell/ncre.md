2025年3月计算机等级考试 三级Linux应用与开发技术考题

1.三个脚本文件的内容如下：

```shell
$ cat exc1.sh 
#!/bin/bash
export score=100
echo "====="
./exc2.sh
echo "====="
./exc3.sh

$ cat exc2.sh 
#!/bin/bash
echo 2:"$score"
export score=90
./exc3.sh

$ cat exc3.sh 
#!/bin/bash
echo 3:"$score"
```

请给出exc1.sh的执行结果：

```shell
$ ./exc1.sh 
=====
2:100
3:90
=====
3:100
```

> 说明：使用export设置的环境变量只在当前shell及其子shell中可用。

2.请给出下列命令的输出结果：

```shell
$ touch file1 file2 file3 file4
$ echo a > file1
$ echo -n a > file2
$ for ((i = 0; i < 4096; i++)) do echo a >> file3; done
$ for ((i = 0; i < 4096; i++)) do echo -n a >> file4; done
$ wc -c file? | sort -n
```

执行结果如下：

```shell
$ wc -c file? | sort -n
    1 file2
    2 file1
 4096 file4
 8192 file3
12291 total
```

* 说明：

①echo：默认情况下，echo会添加换行符，使用`-n`选项后不会添加换行符；

②wc：`-c`选项用于统计文件的字节数，当对多个文件进行统计时，wc会额外输出一个`total`行；

③sort：默认情况下，sort会采用升序排序，`-n`表示按字符串的数值排序

