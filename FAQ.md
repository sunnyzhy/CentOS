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
