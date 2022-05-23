有没有办法在不输入密码的情况下，通过SSH登陆登录服务器呢？

### 配置步骤

1.生成秘钥

首先，查看本机是否已经生成过秘钥：

```shell
hegongshan@hgs:~$ ls ~/.ssh/id_*
ls: cannot access '/home/hegongshan/.ssh/id_*': No such file or directory
```

如果出现了上述问题，则说明这台机器还没有生成过秘钥。此时，可以使用`ssh-keygen`命令生成秘钥：

```shell
hegongshan@hgs:~$ ssh-keygen -t rsa
Generating public/private rsa key pair.
```

其中，`-t`选项用于指定加密算法。

执行完上述操作后，`~/.ssh`目录下将会生成两个文件：`id_rsa.pub`和`id_rsa`。其中，`id_rsa.pub`存储的是公钥，而`id_rsa`存储的则是私钥。

此时，如果我们再次查看秘钥，将会得到如下结果：

```shell
hegongshan@hgs:~$ ls ~/.ssh/id_*
/home/hegongshan/.ssh/id_rsa  /home/hegongshan/.ssh/id_rsa.pub
```

2.将公钥复制到服务器上

ssh中有个一个工具ssh-copy-id，用于复制公钥：

```
hegongshan@hgs:~$ ssh-copy-id 用户名@IP地址
```

按下Enter键后，终端将会提示输入用户密码。

认证通过后，公钥将被追加到服务器的`~/.ssh/authorized_keys`中。

除了`ssh-copy-id`以外，我们还可以通过如下的方式将公钥复制到服务器上：

```shell
cat ~/.ssh/id_rsa.pub | \
ssh 用户名@IP地址 ”mkdir -p ~/.ssh && chmod 700 ~/.ssh && \
cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys“
```

注意：`~/.ssh/authorized_keys`的访问权限必须为`rw-------`（600），即只有其所有者才有读写权限。

3.修改服务器配置

首先，编辑服务器的sshd配置文件`/etc/ssh/sshd_config`：

```shell
vim /etc/ssh/sshd_config
```

开启公钥认证：

```shell
PubkeyAuthentication yes
```

然后，重启sshd服务：

```shell
# Ubuntu
sudo systemctl restart ssh

# CentOS
sudo systemctl restart sshd
```

现在，我们不需要输入密码，就可以直接登录服务器了。

4.测试免密码登录

```shell
ssh 用户名@IP地址
```

默认情况下，ssh会使用`~/.ssh/id_rsa`进行认证。我们也可以通过选项`-i`指定私钥的位置：

```shell
ssh -i identity_file 用户名@IP地址
```

### 参考资料

1.Configuring an SSH login without password，

https://www.ibm.com/support/pages/configuring-ssh-login-without-password

2.How to Use SSH Login Without Key or Password，

https://www.techjunkie.com/ssh-login-without-key-password/
