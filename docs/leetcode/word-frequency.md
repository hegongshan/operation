[192. 统计词频](https://leetcode.cn/problems/word-frequency/)

写一个 bash 脚本以统计一个文本文件 words.txt 中每个单词出现的频率。

为了简单起见，你可以假设：

* `words.txt`只包括小写字母和 `' '` 。
* 每个单词只由小写字母组成。
* 单词间由一个或多个空格字符分隔。

**示例:**

假设`words.txt`内容如下：

```
the day is sunny the the
the sunny is is
```

你的脚本应当输出（以词频降序排列）：

```
the 4
is 3
sunny 2
day 1
```

**说明:**

* 不要担心词频相同的单词的排序问题，每个单词出现的频率都是唯一的。
* 你可以使用一行`Unix pipes`实现吗？

```bash
cat words.txt | tr -s " " "\n" | sort | uniq -c | sort -k 1nr,2r | awk '{print $2 " " $1}'

# cat words.txt | tr -s " " "\n" | sort | uniq -c | sort -k 1nr,2r | awk '{printf "%s %s\n", $2, $1}'

# cat words.txt | xargs | sed 's/\s/\n/g' | sort | uniq -c | sort -k 1nr,2r | awk '{print $2 " " $1}'
```
