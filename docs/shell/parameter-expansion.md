# 参数扩展（Parameter Expansion）



|     参数表达式     | 描述                                                         |
| :----------------: | ------------------------------------------------------------ |
| ${parameter:-word} | 如果parameter未设置或者为空，返回word；否则，返回parameter的值 |
| ${parameter:=word} |                                                              |
| ${parameter#word}  | 从parameter前面删除word，使用最短匹配（shortest matching pattern） |
| ${parameter##word} | 从parameter前面删除word，使用最长匹配（longest matching pattern） |
| ${parameter%word}  | 从parameter后面删除word，使用最短匹配（shortest matching pattern） |
| ${parameter%%word} | 从parameter后面删除word，使用最长匹配（longest matching pattern） |



```bash
$ echo ${name:-hgs}
hgs
```

