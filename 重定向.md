# command > /dev/null 2>&1 命令详解

## 1. 伪设备
在类 unix 系统系统上的设备节点不一定必须与物理设备相对应。缺少此对应关系的节点构成伪设备组。它们提供操作系统处理的各种功能。一些最常用（基于字符的）伪设备包括：

- /dev/null - 通常被用于丢弃不需要的输出流。
- /dev/zero - /dev/zero 是一个特殊的文件，当你读它的时候，它会提供无限的空字符(NULL, ASCII NUL, 0x00)。其中的一个典型用法是用它提供的字符流来覆盖信息，另一个常见用法是产生一个特定大小的空白文件。
- /dev/full - /dev/full（常满设备）是一个特殊设备文件，总是在向其写入时返回设备无剩余空间（错误码为ENOSPC），读取时则与/dev/zero相似，返回无限的空字符(NULL, ASCII NUL, 0x00)。这个设备通常被用来测试程序在遇到磁盘无剩余空间错误时的行为。
- /dev/random[urandom] - /dev/random是一个特殊的设备文件，可以用作随机数发生器或伪随机数发生器。它允许程序访问来自设备驱动程序或其它来源的背景噪声。常用作随机数发生器。

## 2. 文件描述符
在类 unix 系统中，当系统启动时就已经有三个标准文件流以及三个文件描述符被预先占用了，其对应关系如下：

|名称|文件描述符|操作符|
|--|--|--|
|标准输入(STDIN)|0|<, <<|
|标准输出(STDOUT)|1|>, >>, 1>, 1>>|
|标准错误输出(STDERR)|2|2>, 2>>|

标准输出写法1:

```bash
echo "hello" > t.log
```

标准输出写法2:

```bash
echo "hello" 1> t.log
```

当我们执行某个命令时，如果该命令执行正确并且有输出，则该命令的输出是在标准输出设备。如果该命令执行失败，类 unix 系统则会给出提示，该提示在标准错误设备输出。

例如：
```bash
# pwd
/root

# pwdd
bash: pwdd: command not found...
Similar command is: 'pwd'
```

## 3. 重定向
重定向是把```标准输出```定向到文件或者标准流，重定向符有两个：

- \> 以覆盖的方式重定向输出到文件
   ```bash
   # pwd > pwd.log
   
   # cat pwd.log
   /root
    
   # pwd > pwd.log
   
   # cat pwd.log
   /root
   ```

- \>\> 以追加的方式重定向输出到文件
   ```bash
   # pwd >> pwd.log
   
   # cat pwd.log
   /root
   /root
   
   # pwd >> pwd.log
   
   # cat pwd.log
   /root
   /root
   /root
   ```

如果输入了错误的命令，屏幕就会输出标准错误；如果不想将标准错误输出到屏幕上，就需要使用合并重定向技术 ```>&``` ，如: ```2>&1``` ，将标准输出和标准错误输出合并后重定向，这样的话，标准输出和标准错误输出都会输出到文件。

1. 标准错误不会输出到文件
   ```bash
   # pwdd
   bash: pwdd: command not found...
   Similar command is: 'pwd'
   
   # pwdd > pwd.log
   bash: pwdd: command not found...
   Similar command is: 'pwd'
   
   # cat pwd.log
   ```

2. 把标准输出和标准错误输出合并后重定向到文件
   ```bash
   # pwdd > pwd.log 2>&1
   
   # cat pwd.log 
   bash: pwdd: command not found...
   Similar command is: 'pwd'
   ```

## 4. command > /dev/null 2>&1

该命令将标准输出和标准错误输出合并后重定向到伪设备 /dev/null ，也就是不会有任何日志输出到屏幕或文件。

可以通过 $? 查看命令的返回值：0 代表正常，其他非 0 代表异常。

```bash
# pwd > /dev/null 2>&1

# echo $?
0

# cat /dev/null

# cd /dev/null
-bash: cd: /dev/null: Not a directory

# pwdd > /dev/null 2>&1

# echo $?
127

# cat /dev/null

# cd /dev/null
-bash: cd: /dev/null: Not a directory
```
