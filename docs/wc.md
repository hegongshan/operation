wc：word, line, character, and byte count

```sh
wc [-clmw] [file ...]
```

* c：byte，统计字节数。该选项会取消它前面的m。当采用uft-8编码时，一个汉字占用三个字节。

```sh
hgs:Desktop hegongshan$ cat test.txt 
My name is He Gongshan.	# 24个字节
湖北 武汉 		# 4个汉字占用12个字节，空格和换行2个字节
hgs:Desktop hegongshan$ wc -c test.txt 
      38 test.txt
```

* l：line，统计行数。该选项统计的是换行符。最后一个换行符之后的字符不会被统计。

```sh
hgs:Desktop hegongshan$ cat test.txt 
My name is He Gongshan.
湖北 武汉 			# 末尾有换行符
hgs:Desktop hegongshan$ wc -l test.txt 
       2 test.txt
hgs:Desktop hegongshan$ cat test2.txt 
My name is He Gongshan.
湖北 武汉hgs:Desktop hegongshan$ # 末尾没有换行符
hgs:Desktop hegongshan$ wc -l test2.txt 
       1 test2.txt
```

* m：character，统计字符数。该选项会取消它后面的c。

```sh
hgs:Desktop hegongshan$ cat test.txt 
My name is He Gongshan. # 24个字符（末尾有一个换行符）
湖北 武汉 		# 6个字符（末尾有一个换行符）
hgs:Desktop hegongshan$ wc -m test.txt 
      30 test.txt
```

* w：word，统计单词数。按照英语的习惯，空格隔开算一个单词。

```sh
hgs:Desktop hegongshan$ cat test.txt 
My name is He Gongshan. # 5个单词
湖北 武汉 		# 2个单词
hgs:Desktop hegongshan$ wc -w test.txt 
       7 test.txt
```

注意，c和m不能同时使用。按照行数、单词数、字节数/字符数以及文件名的顺序输出。

默认情况，wc命令将使用c、l和w三个参数。

```sh
hgs:Desktop hegongshan$ cat test.txt
My name is He Gongshan.
湖北 武汉
hgs:Desktop hegongshan$ wc test.txt
       2       7      38 test.txt
```

当统计多个文件时，除了输出每个文件的各项统计数据外，还将输出总共的统计数据。

```sh
hgs:Desktop hegongshan$ cat test.txt hgs.txt
My name is He Gongshan.
湖北 武汉
Wuhan Hubei China
中国
hgs:Desktop hegongshan$ wc test.txt hgs.txt
       2       7      38 test.txt
       2       4      25 hgs.txt
       4      11      63 total
```



