# linux 命令 - awk

## 命令格式

```
awk 选项 '模式或条件 {编辑指令}' 文件 1 文件 2 …
```

## 记录与字段

awk 一次从文件中读取一条记录，并将记录存储在列变量 ```0``` 中。记录被分割为字段并存储在 ```1,2,...,NF``` 中(默认使用空格或制表符为分隔符)。

内建变量 NF 为记录的列数。

示例：

- 读取输入行并输出第一列，第二列，第三列：
    ```bash
    # echo hello the world | awk '{print $1,$2,$3}'
    hello the world
    ```
- 读取输入行并输出该行：
    ```bash
    # echo hello the world | awk '{print $0}'
    hello the world
    ```
- 读取输入行并输出该行的列数：
    ```bash
    # echo hello the world | awk '{print NF}'
    3
    ```
- 读取输入行并输出该行的最后一列：
    ```bash
    # echo hello the world | awk '{print $NF}'
    world
    ```

## 字段分隔符

awk 读取数据，默认以空格或制表符作为分隔符，但可以通过 ```-F``` 或 ```FS(field separator)``` 变量来改变分隔符。

示例：

```bash
# echo hello:the:world | awk -F ':' '{print $2}'
the

# echo hello:the:world | awk 'BEGIN {FS=":"} {print $2}'
the
```

指定多个分隔符：

```bash
# echo 'hello the:word,!' | awk 'BEGIN {FS="[:, ]"} {print $1,$2,$3,$4}'
hello the word !
```

## 内建变量

- ```FS```: 列分割符。指定每行文本的字段分隔符，默认为空格或制表位。与 ```-F```作用相同
- ```FNR```: 当前输入文档的当前记录编号，尤其当有多个输入文档时有用
- ```NF```: 当前记录的列数
- ```NR```: 当前记录的行号
- ```FILENAME```: 当前输入文档的名称
- ```RS```: 行分隔符，默认为换行符 ```\n```

示例：

```bash
# cat awk.txt
1  one    100
2  two    200
3  three  300
4  four   400
5  five   500
```

- 输出每行的行号：
```bash
# awk '{print NR}' awk.txt
1
2
3
4
5
```
- 输出每行列数：
```bash
# awk '{print NF}' awk.txt 
3
3
3
3
3
```
- 输出每行的第一列的内容：
```bash
# awk '{print $1}' awk.txt 
1
2
3
4
5
```
- 输出每行的最后一列的内容：
```bash
# awk '{print $NF}' awk.txt 
100
200
300
400
500
```
- 输出第一行的内容：
```bash
# awk 'NR==1 {print}' awk.txt 
1  one    100
```
- 输出第一行第二列的内容：
```bash
# awk 'NR==1 {print $2}' awk.txt 
one
```
- 输出第一行最后一列的内容：
```bash
# awk 'NR==1 {print $NF}' awk.txt 
100
```
- 输出第二行以后的内容：
```bash
# awk 'NR>=3 {print $0}' awk.txt 
3  three  300
4  four   400
5  five   500
```
- 输出最后一行的内容：
```bash
# awk 'END {print $0}' awk.txt
5  five   500
```
- 输出最后一行最后一列的内容：
```bash
# awk 'END {print $NF}' awk.txt
500
```

示例：

```bash
# cat awk1.txt
This is a test file. 
Welcome to Jacob's Class.

# cat awk2.txt
Hello the world. 
Wow! I'm overwhelmed. 
Ask for more. 
```

- 输出当前文档的当前行行号：
    ```bash
    # awk '{print FNR}' awk1.txt awk2.txt
    1
    2
    1
    2
    3
    ```
- 将两个文档作为一个整体的输入流，通过 NR 输入当前行行号：
    ```bash
    # awk '{print NR}' awk1.txt awk2.txt
    1
    2
    3
    4
    5
    ```
- awk1.txt 文档的第一行有 5 列，第二行有 4 列：
    ```bash
    # awk '{print NF}' awk1.txt
    5
    4
    ```

## 表达式与操作符

示例：

- 操作符：
    ```bash
    # echo | awk 'x=2 {print x+3}'
    5
    
    # echo | awk 'x=2,y=3 {print x*2, y*3}'
    4 9
    ```
- 列出 ID 号大于 500 的用户名：
    ```bash
    # awk -F: '$3>500 {print $1}' /etc/passwd
    ```

## 条件及循环

### if

```bash
# df | grep "boot" | awk '{if($4<20000) print "Alart"; else print "OK"}'
OK

# awk -F: '{if($3<1000){x++} else{y++}} END{print "系统用户个数:"x"","普通用户个数:"y""}' /etc/passwd
系统用户个数:54 普通用户个数:2
```

### for

```bash
# awk 'BEGIN{a[0]=11;a[1]=12;print a[0],a[1]}'

# awk 'BEGIN{a[0]=11; a[1]=12; a[2]=13; for(i in a) {print i,a[i]}}'
0 11
1 12
2 13

# awk 'BEGIN{ for (i=1;i<=5;i++) {print i}}'
1
2
3
4
5

# awk -F: '{for(i=1;i<=NF;i++) {if($i=="root") x++}} END {print x}' /etc/passwd
2

# whereis mysql
mysql: /usr/bin/mysql /usr/lib64/mysql /usr/share/man/man1/mysql.1.gz

# whereis mysql | awk '{for(i=2;i<=NF;i++)print $i}'
/usr/bin/mysql
/usr/lib64/mysql
/usr/share/man/man1/mysql.1.gz
```

### while

```bash
# awk 'BEGIN{ i=1; while(i<=5) {print i;i++}}'
1
2
3
4
5

# awk 'BEGIN{
> i=0;
> while(i<=5) {
> i++;
> if(i==3) {continue};
> print i
> };
> }
> END {print "END"}' /dev/null
1
2
4
5
6
END
```

## 函数

```length()``` 显示文档每行字符串的长度。

```bash
# cat awk.txt 
1  one    'this is the first row.'
2  two    'this is the second row.'
3  three  'this is the third row.'
4  four   'this is the fourth row.'
5  five   'this is the fifth row.'

# awk '{print length()}' awk.txt
34
35
34
35
34
```
