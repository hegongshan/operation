### 让当前进程休眠

```bash
sleep <seconds>
```

例如：让当前进程休眠1s

```bash
sleep 1s
sleep 1m
sleep 1h
sleep 1d
```

每隔1s输出一次内存的使用情况：

```bash
while true; do
    sleep 1s
    free -h >> mem.txt
done	
```

### 等待某个进程或作业结束

等待某个进程或作业结束，再执行后续代码

```bash
wait [<pid>|<jobid>]
```

例如：等待最后一个后台进程结束

```bash
wait $!
```
