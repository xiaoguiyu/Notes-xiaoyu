



## Windows系统命令

### 进程

下面命令为 查找到 端口 1099 的信息

```sh
netstat -aon | find "1099"
```

![](windows%E7%9B%B8%E5%85%B3.assets/%E7%AB%AF%E5%8F%A3%E5%8F%B7%E5%AF%B9%E5%BA%94pid.png)

下面命令用来查找 pid 所对应的进程的信息

```shell
tasklist | find "3856"
```



#### 杀死进程

可以根据pid 来杀死 占用 端口的进程, 使用方法如下

```sh
taskkill /f /pid 3856
```



