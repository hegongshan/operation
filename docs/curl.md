curl，全称为client URL，官网为https://curl.se。

```shell
curl www.hegongshan.com
```

### 设置User-Agent

`-A, --user-agent <name>`，指定HTTP请求头中的用户代理字段：User-Agent。

```shell
curl -A 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36' www.baidu.com
```

### 设置请求头

```shell
-H, --header <header>
```



```shell
curl -H 'User-Agent: php/1.0' 
```

### 发送HTTP请求

设置HTTP请求方式

```shell
-X, --request <command>
```

发送POST请求数据

```shell
-d, --data <data>
```

### 重定向

-L, --location

```shell
curl -L www.hegongshan.com
```

