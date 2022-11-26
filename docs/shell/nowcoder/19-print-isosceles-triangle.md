SHELL19 打印等腰三角形

### 描述
编写一个shell脚本，输入正整数n，打印边长为n的等腰三角形。

### 示例：
输入：5
输出：

```
    *
   * *
  * * *
 * * * *
* * * * *
```

### 题解

1.使用原生的for循环+seq

```bash
#!/bin/bash
read n
i=1
while [ $i -le $n ]; do
    if [ $i -lt $n ]; then
        for j in $(seq 1 $((n - i)) ); do
            printf " " 
        done
    fi  
    
    for j in $(seq 1 $i); do
        printf "* "
    done
    printf "\n"

    i=$((i + 1))
done
```

2.使用C语言风格的for循环

```bash
#!/bin/bash
read n
for ((i = 1; i <= n; i++)); do
    # 打印前面的空格
    for ((j = 0; j < n - i; j++)); do
        printf " "
    done
    
    # 打印*
    for ((j = 0; j < i; j++)); do
        printf "* "
    done
    printf "\n"
done
```

3.使用awk

```bash
read n
awk -v n=$n 'BEGIN {
    for (i = 1; i <= n; i++) {
        for (j = 0; j < n - i; j++) {
            printf " "
        }
        for (j = 0; j < i; j++) {
            printf "* "
        }
        printf "\n"
    }
}' 
```

