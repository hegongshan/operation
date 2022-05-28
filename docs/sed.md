sed（**s**tream **ed**itor）是一个命令行文本编辑工具，可以用于处理一系列重复的文本编辑任务。

```bash
sed command file
```

### 替换

```bash
s/regexp/replacement/
```

例如，删除每行开头的多个空格

```bash
sed 's/^\s\+//g' cpu.txt
```

### 打印

```bash
sed -n '1,10p' file.txt
```
