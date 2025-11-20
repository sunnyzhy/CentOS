# linux 命令 - shell 脚本

## /bin/bash 和 /bin/sh 的区别

1. ```/bin/sh``` 是 ```/bin/bash``` 的软连接，在一般的 linux 系统当中，使用 sh 调用执行脚本相当于打开了 bash 的 POSIX 标准模式，也就是说 ```/bin/sh``` 相当于 ```/bin/bash --posix```
2. ```/bin/sh``` 执行过程中，若出现命令执行失败，则会停止执行；```/bin/bash``` 执行过程中，若命令执行失败，仍然会继续执行

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

批量 kill 进程:

```bash
ps -ef | grep st- | grep -v grep | awk '{print $2}' | xargs kill -9
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

同时指定 mindepth 和 maxdepth 缩小遍历的范围:

```bash
# find $dir -mindepth 1 -maxdepth 1
/usr/local/find/aa
/usr/local/find/bb
```

## 批量结束进程

### 命令行

```bash
kill -9 `ps -ef | grep process- | awk 'NR>1 {print line} {line=$0}' | awk '{print $2}'`
```

### shell 脚本

```bash
#/bin/sh

PID=`ps -ef | grep process- | awk 'NR>1 {print line} {line=$0}' | awk '{print $2}'`
for p in $PID
do
   kill -s 9 $p
done

echo "ok"
```

## 综合应用
```bash
#/bin/sh

# 结束名称前缀为 st- 的 java 进程
PID=$(ps -ef | grep st- | grep -v grep | awk '{print $2}')
for pid in $PID
do
	kill -9 $pid
done

# 存储 java 文件(jar) 的目标目录
target=/usr/java/app

# 删除目标目录里的旧 jar 文件
for dir in $target/*
do
	if test -d $dir
	then
		if test[ $dir == */st-* ] # 只删除名称前缀为 st- 的目录里的 jar 文件
		then
			if test[ $dir == */st-ignore1 || $dir == */st-ignore2 || $dir == */st-ignore3 ] # 忽略指定名称前缀的 jar 文件
			then
				continue
			fi
			for d in $dir/*
			do
				if test -d $d
				then
					if test[ $d == */log ] # 删除 log 目录
					then
						rm -rf $d
					fi
				fi
				if test -f $d
				then
					if test[ $d == *.log || $d == *.jar* ] # 只删除 log 文件和 jar 文件，重要：如果有 pem, lic 文件，则不能删除
					then
						rm -rf $d
					fi
				fi
			done
		fi
	fi
done

# 把源文件复制到目标目录里
roots=/usr/local/deploy_app
for dir in $roots/*
do
	if test -d $dir
	then
		if test ! -d $dir/target 
		then
			# 如果源目录里没有 target 目录，就直接复制源文件到目标目录里
			jar=`find $dir -mindepth 1 -maxdepth 1 -name "*.jar" -type f`
			if test ! -z $jar 
			then
				cp -r $dir/ $target
				continue
			fi  fi
			# 处理源目录里的 target 目录，视实际情况来定，如果目标目录里需要 target 目录，就不用执行以下两行命令
			mv $dir/target/*.jar $dir/
			rm -rf $dir/target
			# 复制源文件到目标目录里
			cp -r $dir $target
		fi
	done

	# 启动名称前缀为 st- 的 java 进程
	apps=`find $target -mindepth 1 -maxdepth 1 -type d`
	for a in $apps
	do
		if test[ "$(ls -A $a)" == "" || $a == */IgnoreDir ] # 如果是空目录或需要忽略启动的目录，就不执行启动命令
		then
			continue
		fi
		cd $a
		app=`find ./ -mindepth 1 -maxdepth 1 -name "*.jar" -type f` # 只在当前目录下查找 jar 文件，不用递归子级目录
		if test ! -z "$app"  # 如果文件大小不为 0
		then
			if test[ $app == */st-app-* ] # 如果 jar 文件的名称前缀为 st-app-, 就把 jvm 的启动内存设置为 512m
			then
				nohup java -jar -XX:+HeapDumpOnOutOfMemoryError -Xmx512m -Xms512m $app > /dev/null 2>&1 &
			else # 否则, 就把 jvm 的启动内存设置为 256m
				nohup java -jar -XX:+HeapDumpOnOutOfMemoryError -Xmx256m -Xms256m $app > /dev/null 2>&1 &
			fi
		fi
	done

	echo "ok!"
```
