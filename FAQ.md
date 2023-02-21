# FAQ

## 1 make: Nothing to be done for `all' 解决方法

这句提示是说你已经编译好了，而且没有对代码进行任何改动。

若想重新编译，可以先删除以前编译产生的目标文件：

```bash
# make clean
```

然后再

```bash
# make
```

## 2 Another app is currently holding the yum lock; waiting for it to exit...

通过执行如下命令强制解除占用:

```bash
# rm -rf /var/run/yum.pid
```

## 3 Someone could be eavesdropping on you right now (man-in-the-middle attack)!It is also possible that a host key has just been changed.

```bash
# ssh-keygen -R 主机名或主机IP
```

## 4 使用 vim 时，键盘输入没有反应

问题原因: 不小心按了 ```Ctrl + s```，vim 停止向终端输出，导致不能输入任何字符

解决方法: 按下 ```Ctrl + q``` 退出这种状态

## 5 找不到 Network 的 Wird 可视化配置项

问题描述: 

1. ```systemctl restart network``` 重启 network 报错
2. 找不到 Network 的 Wird 可视化配置项

解决方法:

```bash
mv /var/lib/NetworkManager /var/lib/NetworkManager.bak

reboot
```

## 6 Entering emergency mode.Exit the shell to continue

```bash
# journalctl
XFS(xxx)....

# xfs_repair -v -L /dev/xxx

# reboot
```

***注: ```xfs_repair``` 的目录就是 ```XFS``` 括号里的内容。***
