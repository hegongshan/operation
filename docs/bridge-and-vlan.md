### 网桥

安装网桥管理工具：

* CentOS

```bash
yum install -y bridge-utils
```

* Ubuntu

```bash
apt install -y bridge-utils
```

创建网桥：

```bash
brctl addbr <bridge>
```

将网卡添加到网桥中：

```bash
brctl addif <bridge> <device>
```

### 虚拟网卡

安装虚拟网卡管理工具：

* CentOS

```bash
yum install -y vconfig
```

* Ubuntu

```bash
apt install -y vlan
```

```bash
vconfig add [interface-name] [vlan_id]
vconfig rem [vlan-name]
```

