sort是一个强大的排序工具。

常用的选项：

-t, --field-separator SEP：设置分隔符

-k, --key KEYDEF: 设置待排序的键。

KEYDEF的完整格式为`F[.C][OPTS][,F[.C][OPTS]]`。其中，F表示第F个字段，C表示从该字段的第C个字符开始，`OPTS`指定了排序选项。

> KEYDEF is `F[.C][OPTS][,F[.C][OPTS]]` for start and stop position, where F is a field number and C a character position in the field; both are origin 1, and the stop position defaults to the line's end. If neither  -t nor -b is in effect, characters in a field are counted from the beginning of the preceding whitespace. OPTS is one or more single-letter ordering options [bdfgiMhnRrV], which override global ordering options for that key. If no key is given, use the entire line as the  key.

-b，--ignore-leading-blanks：忽略前导0.

-n, --numeric-sort：根据字符串的数值进行排序。例如，按照字典序排序时，字符串`2`大于`11`；而按照数值进行排序时，`2`小于`11`。

-h, --human-numeric-sort

-r, --reverse：降序排列。

```shell
hgs:Desktop hegongshan$ cat douban.txt 
天空之城,1986,9.1,724101
哈尔的移动城堡,2004,9.1,873641
龙猫,1988,9.2,1111532
千与千寻,2001,9.4,1968140
起风了,2013,8.1,215979
你的名字,2016,8.5,1207085
秒速五厘米,2007,8.3,520484
天气之子,2019,7.1,329731
```

实例

* 以逗号作为分隔符，按照第4个字段（评论数）降序排列

```bash
hgs:Desktop hegongshan$ sort -t "," -k 4r douban.txt
哈尔的移动城堡,2004,9.1,873641
天空之城,1986,9.1,724101
秒速五厘米,2007,8.3,520484
天气之子,2019,7.1,329731
起风了,2013,8.1,215979
千与千寻,2001,9.4,1968140
你的名字,2016,8.5,1207085
龙猫,1988,9.2,1111532
```



```bash
hgs:Desktop hegongshan$ sort -t "," -k 4nr douban.txt
千与千寻,2001,9.4,1968140
你的名字,2016,8.5,1207085
龙猫,1988,9.2,1111532
哈尔的移动城堡,2004,9.1,873641
天空之城,1986,9.1,724101
秒速五厘米,2007,8.3,520484
天气之子,2019,7.1,329731
起风了,2013,8.1,215979
```

* 按照评分降序排序，当评分相同时，按照评论数升序排列

```bash
hgs:Desktop hegongshan$ sort -t "," -k 3nr -k 4n douban.txt 
千与千寻,2001,9.4,1968140
龙猫,1988,9.2,1111532
天空之城,1986,9.1,724101
哈尔的移动城堡,2004,9.1,873641
你的名字,2016,8.5,1207085
秒速五厘米,2007,8.3,520484
起风了,2013,8.1,215979
天气之子,2019,7.1,329731
```

