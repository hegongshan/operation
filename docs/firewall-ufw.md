ufw（Uncomplicated FireWall）是Ubuntu的默认防火墙。

* 查看防火墙状态，包括防火墙是否启动、开放和关闭的端口等信息

```bash
ufw status
```

* 开启/关闭防火墙

```bash
ufw enable

ufw disable
```

* 开放端口

```bash
ufw allow [port]
```

* 关闭端口

```bash
ufw deny [port]
```

