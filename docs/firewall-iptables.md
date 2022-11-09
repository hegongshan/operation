iptables是Linux中的一个包过滤工具。

### 基础概念

-t：指定表

* filter：默认表。
* nat：全称为Network Address Translation，网络地址转换。

#### 链中的规则

|        源地址        | 源地址端口 |         目的地址          | 目的地址端口 |      协议      |            Target            |
| :------------------: | :--------: | :-----------------------: | :----------: | :------------: | :--------------------------: |
| -s, --source address |  --sport   | -d, --destination address |   --dport    | -p, --protocol | ACCEPT、DROP、REJECT、RETURN |

示例：

```shell
sudo iptables -A INPUT -d 192.168.1.0/24 --dport 80 -p tcp -j ACCEPT
```

### 查看链和规则

* 查看链

-L，--list [chain]：

示例：

```shell
sudo iptables -n -L --line-numbers
```

-n，--numeric：以数字的形式输出地址和端口号

--line-numbers：打印行号

* 查看规则

```shell
-S, --list-rules [chain]
```

### 添加链和规则

* 添加链

```shell
-N, --new-chain chain
```

* 在链头插入规则

```shell
-I, --insert chain [rulenum] rule-specification
```

* 在链尾追加规则

```shell
-A, --append chain rule-specification
```

### 删除链和规则

* 删除链

```shell
-X, --delete-chain [chain]
```

示例：

```shell
sudo iptables -X DOCKER
```

* 删除链中的规则

```shell
-D, --delete chain rule-specification

-D, --delete chain rulenum
```

* 清空规则：删除所有规则

```shell
-F, --flush [chain]
```

* 设置链的默认动作

```bash
$ iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination 

Chain FORWARD (policy DROP)
target     prot opt source               destination 

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

-P, --policy chain target

```bash
$ iptables -P INPUT DROP
```

### 网络地址转换

Network Address Translation (NAT)

* 源地址转换：适用于多台内网主机通过相同的公网IP访问互联网

```bash
$ iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.0/24 -j SNAT --to-source 10.190.2.5 
# 如果IP不是固定的，需要使用MASQUERADE自动获取IP
$ iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.0/24 -j MASQUERADE
```

* 目的地址转换：

```bash
$ iptables -t nat -A PREROUTING -i eth0 -d 10.190.2.5 --dport 80 -j DNAT --to-destination 192.168.1.24:80
```



