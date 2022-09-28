ssh-agent，认证代理

1.启动ssh-agent

2.添加私钥

```bash
ssh-add <private key>
```

3.配置ssh

```bash
vim ~/.ssh/config
```

添加如下内容：

```bash
Host *
    ForwardAgent yes
```

