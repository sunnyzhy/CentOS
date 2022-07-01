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
