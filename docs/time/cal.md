cal是日历calendar的简写。

<!--more-->

1.默认情况下，只输出当前月份

```bash
cal
```

2.输出当前月份及之前的n个月

```bash
cal -B n
```
其中，B表示Before。

3.输出当前月份及之后的n个月

```bash
cal -A n
```
其中，A表示After。

4.只输出某年的某月

```bash
cal [[month] year]
```
其中，month是可选的，不加month，表示输出全年的日历。

例如，输出2018年9月：

```bash
[hegongshan@hgs ~]$ cal 9 2018
      九月 2018         
日 一 二 三 四 五 六  
                   1  
 2  3  4  5  6  7  8  
 9 10 11 12 13 14 15  
16 17 18 19 20 21 22  
23 24 25 26 27 28 29  
30  
```
