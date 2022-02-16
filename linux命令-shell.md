# linux命令-shell

## 1 查找 jar 进程 ID，并杀死进程

假如 jar 文件都是以 ```st-``` 开头。

```bash
#!/bin/sh

PID=$(ps -ef | grep st- | grep -v grep | awk '{print $2}')
echo $PID
echo "---------------"

for pid in $PID
do
  #kill -9 $pid
  echo "killed $pid"
done
echo "---------------"
```

## 2 find

创建目录:

```bash
# mkdir -p /usr/local/find/{aa/aa01,bb}

# dir=/usr/local/find
```

### 2.1 depth

先输出子目录，再依次输出上级目录，直到最顶层:

```bash
# find $dir -depth
/usr/local/find/aa/aa01
/usr/local/find/aa
/usr/local/find/bb
/usr/local/find

# find $dir -depth ! -empty
/usr/local/find/aa
/usr/local/find
```

先输出最顶层目录，再依次输出子级目录:

```bash
# find $dir
/usr/local/find
/usr/local/find/aa
/usr/local/find/aa/aa01
/usr/local/find/bb

# find $dir ! -empty
/usr/local/find
/usr/local/find/aa
```

### 2.2 mindepth

指定遍历的最小深度（最小目录层级）。

```-mindepth n```:

- n = 0: 遍历顶层目录、一级目录、二级目录、...、N 级目录
- n = 1: 遍历一级目录、二级目录、...、N 级目录
- n = 2: 遍历二级目录、...、N 级目录

先输出子目录，再依次输出上级目录，直到最顶层:

```bash
# find $dir -depth -mindepth 0
/usr/local/find/aa/aa01
/usr/local/find/aa
/usr/local/find/bb
/usr/local/find

# find $dir -depth -mindepth 1
/usr/local/find/aa/aa01
/usr/local/find/aa
/usr/local/find/bb

# find $dir -depth -mindepth 2
/usr/local/find/aa/aa01
```

先输出最顶层目录，再依次输出子级目录:

```bash
# find $dir -mindepth 0
/usr/local/find
/usr/local/find/aa
/usr/local/find/aa/aa01
/usr/local/find/bb

# find $dir -mindepth 1
/usr/local/find/aa
/usr/local/find/aa/aa01
/usr/local/find/bb

# find $dir -mindepth 2
/usr/local/find/aa/aa01
```

### 2.3 maxdepth

指定遍历的最大深度（最大目录层级）。

```-maxdepth n```:

- n = 0: 遍历顶层目录
- n = 1: 遍历顶层目录、一级目录
- n = 2: 遍历顶层目录、一级目录、二级目录

先输出子目录，再依次输出上级目录，直到最顶层:

```bash
# find $dir -depth -maxdepth 0
/usr/local/find

# find $dir -depth -maxdepth 1
/usr/local/find/aa
/usr/local/find/bb
/usr/local/find

# find $dir -depth -maxdepth 2
/usr/local/find/aa/aa01
/usr/local/find/aa
/usr/local/find/bb
/usr/local/find
```

先输出最顶层目录，再依次输出子级目录:

```bash
# find $dir -maxdepth 0
/usr/local/find

# find $dir -maxdepth 1
/usr/local/find
/usr/local/find/aa
/usr/local/find/bb

# find $dir -maxdepth 2
/usr/local/find
/usr/local/find/aa
/usr/local/find/aa/aa01
/usr/local/find/bb
```
