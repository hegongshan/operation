iptables是Linux中的一个包过滤工具。

### 基础概念

#### 五张表

-t：指定表

* filter：默认表。
* nat：全称为Network Address Translation，网络地址转换。
* mangle
* raw
* security：用于强制访问控制（Mandatory Access Control，MAC）网络规则。

#### 五条链

```shell
PREROUTING
INPUT
FORWARD
OUTPUT
POSTROUTING
```

#### 链中的规则

|        源地址        | 源地址端口 |         目的地址          | 目的地址端口 |      协议      |            Target            |
| :------------------: | :--------: | :-----------------------: | :----------: | :------------: | :--------------------------: |
| -s, --source address |  --sport   | -d, --destination address |   --dport    | -p, --protocol | ACCEPT、DROP、REJECT、RETURN |

示例：

```shell
sudo iptables -A INPUT -s -d --dport 22 -p tcp -j ACCEPT
```

### 查看链和规则

* 查看链

-L，--list [chain]：。

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

* 插入规则

```shell
-I, --insert chain [rulenum] rule-specification
```

* 追加规则

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

* 清空规则：删除所有的规则

```shell
-F, --flush [chain]
```



