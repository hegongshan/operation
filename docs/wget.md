wget，全称为World Wide Web get，用于从Web中下载文件。

```shell
wget https://www.hegongshan.com/robots.txt
```

常用选项：

* -r：递归下载

* -c：继续下载

* -q, --quiet: 关闭wget的输出

* -O file: 重命名

* -P prefix, --directory-prefix=prefix：指定文件存放的目录，默认为`.`，即当前目录
