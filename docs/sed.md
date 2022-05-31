sed（**s**tream **ed**itor）是一个命令行文本编辑工具，可以用于处理一系列重复的文本编辑任务。

```bash
sed [option] command file
```

常用选项：

* `-e command`：添加command
* `-i`：就地编辑
* `-f command_file`：指定命令文件
* `-n`：不输出。默认情况下，在所有的命令执行完以后，输入的每行将会被输出到标准输出中。

2.`command`的格式为：

```bash
[address1[,address2]]function
```

* 选择要编辑的行，例如：

```bash
sed -n '11p' file.txt
sed -n '3,11p' file.txt
sed -n '3,11!p' file.txt
sed -n '3,+3p' file.txt
sed -n '1~2p' file.txt
sed -n '/^#/p' file.txt
```

### 常用函数

#### 替换

```bash
s/regexp/replacement/flags
```

其中，s表示substitute。

|  标志  | 说明                                         |
| :----: | -------------------------------------------- |
|   g    | 全局替换。默认只替换每行中第一次匹配的部分。 |
|   p    | 到标准输出                                   |
|   i    | 忽略大小写                                   |
|   N    | 只替换每行的第N次匹配                        |
| w file | 将替换结果写入文件中                         |

例如，删除每行开头的多个空格

```bash
sed 's/^\s\+//g' cpu.txt
```

#### 打印

```bash
sed -n '1,10p' file.txt
```

其中，p表示print。

#### 删除

```bash
sed '11d' file.txt
```

其中，d表示delete。
