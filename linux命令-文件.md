# linux 常用的文件命令

## 创建文件目录

```bash
# mkdir zz
```

## 查看目录下文件

```bash
# ls

# ls -a // 显示所有文件及目录

# ls -l // 显示文件名、权限、拥有者、文件大小等

# ls java* // 查找当前目录里的以 java 开关的文件

# ls *.jar // 查找当前目录里的 jar 文件
```

## ls 命令显示文件大小

```bash
# ls -lh // 以适当方式显示文件大小

# ls -l // 以 byte 显示文件大小

# ls -l --block-size=m // 以 M 显示文件大小

# ls -l --block-size=G // 以 G 显示文件大小
```

## 复制文件

```bash
# cp /home/run.sh /usr/local
```

强制覆盖:

```bash
# \cp -rf src dest
```

```bash
# /bin/cp -rf src dest
```

## 修改文件名

```bash
# mv /home/run.sh /home/1.sh
```

## 修改文件夹名

```bash
# mv /home/zz /home/z
```

## 移动文件

```bash
# mv /root/run.sh /usr/local
```

## 移动文件夹

```bash
# mv /home/z /usr/local
```

## 查看当前所在目录

```bash
# cd /usr/local

# pwd
/usr/local
```

## 查看登录用户信息

```bash
# who
root     pts/0        2020-06-10 10:16 (xx-pc)
```

## 显示文件全部内容

```bash
# cat nohup.out
```

## 动态显示文件的内容

```bash
# tail -f -n 30 nohup.out
```

- -f：循环读取
- -n <行数>：显示文件的尾部 n 行内容

## 显示文件前 n 行内容

```bash
# head -n 10 nohup.out
```

## 删除文件

```bash
# rm -rf zz
```

- -r或-R：递归处理，将指定目录下的所有文件与子目录一并处理
- -f：强制删除文件或目录

## 清空文件内容

- 第一种

   ```bash
   # > nohup.out
   ```

- 第二种

   ```bash
      # echo "" > nohup.out
   ```

- 第三种

   ```bash
   # cat /dev/null > nohup.out
   ```

## 服务器之间传输文件

### 传输单个文件

```bash
# scp /usr/local/file1 target_username@target_ip:/usr/local/dir
target_username@target_ip's password:
```

### 传输多个文件

```bash
# scp /usr/local/file1 /usr/local/file2 target_username@target_ip:/usr/local/dir
target_username@target_ip's password:
```

### 传输单个目录

```bash
# scp -r /usr/local/dir1 target_username@target_ip:/usr/local
target_username@target_ip's password:
```

### 传输多个目录

```bash
# scp -r /usr/local/dir1 /usr/local/dir2 target_username@target_ip:/usr/local
target_username@target_ip's password:
```

### 免密码传输文件

1. 在主机 A 上生成配对密钥:
   ```bash
   ssh-keygen -t rsa
   ```
2. 遇到提示回车默认即可，生成的公钥位置:
   ```
   /root/.ssh/id_rsa.pub
   ```
3. 将主机 A 的 ```id_rsa.pub``` 文件复制到主机 B 的 ```~/.ssh/``` 目录中，并改名为 ```authorized_keys```:
   ```bash
   scp /root/.ssh/id_rsa.pub root@192.168.0.10:/root/.ssh/authorized_keys
   ```
   此时在主机 A 中用 SSH 登录主机 B 或向主机 B 拷贝文件，都将不需要密码。

## 压缩/解压文件

### tar.gz

#### 压缩

```bash
# tar -czvf xxx.tar.gz(目标文件) 源文件
```

#### 解压

```bash
# tar -xzvf xxx.tar.gz -C dir
```

### jar/zip/...

#### 压缩

```bash
# cd xxx

# jar -cvf0m xxx.jar ./META-INF/MANIFEST.MF .
```

#### 解压到当前目录

```bash
# unzip xxx.jar
```

#### 解压到指定目录

```bash
# unzip xxx.jar -d xxx
```

## 获取文件名和目录名

### basename 获取文件名

```bash
# var=/dir1/dir2/file.log

# echo $(basename $var)
file.log

# var=/dir1/dir2/file.tar.gz

# echo $(basename $var)
file.tar.gz
```

### dirname 获取目录名

```bash
# var=/dir1/dir2/file.log

# echo $(dirname $var)
/dir1/dir2
```

### ${var#\*.} 取文件的后缀名

删除第一个 ```.``` 及之前的内容。

```bash
# var=/dir1/dir2/file.log

# echo ${var#*.}
log

# var=/dir1/dir2/file.tar.gz

# echo ${var#*.}
tar.gz
```

### {var##\*/} 取文件名

删除最后一个 ```/``` 及之前的内容。

```bash
# var=/dir1/dir2/file.log

# echo ${var##*/}
file.log
```

### ${var##\*.} 取文件的后缀名

删除最后一个 ```.``` 及之前的内容。

```bash
# var=/dir1/dir2/file.log

# echo ${var##*.}
log

# var=/dir1/dir2/file.tar.gz

# echo ${var##*.}
gz
```

### ${var%/\*} 取目录名

删除最后一个 ```/``` 及之后的内容。

```bash
# var=/dir1/dir2/file.log

# echo ${var%/*}
/dir1/dir2
```

### ${var%%.\*} 取文件名（不含后缀名）

删除第一个 ```.``` 及之后的内容。

```bash
# var=/dir1/dir2/file.log

# echo ${var%%.*}
/dir1/dir2/file

# var=/dir1/dir2/file.tar.gz

# echo ${var%%.*}
/dir1/dir2/file
```

注:

- #: 删除第一个匹配字符及之前的内容
- ##: 删除最后一个匹配字符及之前的内容
- %: 删除最后一个匹配字符及之后的内容
- %%: 删除第一个匹配字符及之后的内容

## 目录使用率为 100%

- 使用 ```lsof``` 杀死僵尸进程

   ```bash
      # lsof | grep delete | awk -F ' ' '{ print $2}'|xargs kill -9
   ```

- 使用 ```du -h``` 命令查询大文件

   ```bash
   # du -h -x --max-depth=1
   ```
   进入大文件目录，再执行 ```du -h -x --max-depth=1``` 查出哪个目录占用过多， 进入对应的目录，看是否有可以删除的文件或文件夹，就这样逐层往下查找。

## vim 全选复制

1. 查看是否支持 clipboard

   ```bash
   # vim --version | grep clipboard
   -clipboard         +jumplist          +persistent_undo   +virtualedit
   -ebcdic            -mouseshape        +statusline        -xterm_clipboard
   ```

2. 如果出现 -clipboard，就表示不支持 clipboard

3. 安装 vim-X11

   ```bash
   # yum -y install vim-X11
   
   # alias vim='gvim -v'
   
   # source .bashrc
   ```

4. 查看是否支持 clipboard

   ```bash
   # vim --version | grep clipboard
   +clipboard       +iconv           +path_extra      +toolbar
   +eval            +mouse_dec       +startuptime     +xterm_clipboard
   ```

5. 如果出现 +clipboard，就表示支持 clipboard

6. 在 vim 中全选，区分大小写

   ```bash
   ggVG
   ```

7. 在 vim 中复制

   ```bash
   "+y
   ```

## vim 替换

1. 把当前行的第一个 aa 替换为 bb

   ```bash
   :s/aa/bb/
   ```

2. 把当前行中所有的 aa 替换为 bb

   ```bash
   :s/aa/bb/g
   ```

3. 把每一行的第一个 aa 替换为 bb
   - 方法1

      ```bash
      :%s/aa/bb/
      ```
   - 方法2

      ```bash
      :g/aa/s//bb/
      ```

4. 把每一行中所有的 aa 替换为 bb
   - 方法1

      ```bash
      :%s/aa/bb/g
      ```
   - 方法2

      ```bash
      :g/aa/s//bb/g
      ```

## sed 替换

1. 基本替换（不修改原文件）

   ```bash
   sed 's/old_text/new_text/g' filename
   ```

   - ```s```：表示替换命令
   - ```old_text```：要替换的文本
   - ```new_text```：替换后的文本
   - ```g```：全局匹配（否则只替换每行第一个匹配项）

2. 直接修改原文件（使用 ```-i``` 选项）

   ```bash
   sed -i 's/old_text/new_text/g' filename

   # 带备份的修改（创建 filename.bak）
   sed -i.bak 's/old_text/new_text/g' filename
   ```

3. 使用正则表达式

   ```bash
   # 替换所有数字
   sed 's/[0-9]\+/REPLACED/g' filename
   ```

4. 批量替换多个文件

   ```bash
   # 替换当前目录下所有 .txt 文件
   sed -i 's/old_text/new_text/g' *.txt

   # 递归替换所有文件
   find . -type f -exec sed -i 's/old_text/new_text/g' {} \;

   # 只替换特定类型的文件
   find . -name "*.java" -exec sed -i 's/old_text/new_text/g' {} \;
   ```

5. 包含特殊字符的替换（当替换内容包含 /、$ 等特殊字符时，需要转义或使用其他分隔符）

   ```bash
   # 使用其他分隔符（如 |）
   sed 's|http://old.com|http://new.com|g' filename

   # 转义特殊字符
   sed 's/old\/path/new\/path/g' filename
   ```

## 写文件

## echo

- ```echo > FileName```：覆盖写入
   ```bash
   # echo aa > 1.log
   
   # cat 1.log
   aa
   
   # echo 11 > 1.log
   
   # cat 1.log
   11
   ```

- ```echo >> FileName```：追加写入
   ```bash
   # echo aa > 1.log
   
   # cat 1.log
   aa
   
   # echo 11 >> 1.log
   
   # cat 1.log
   aa
   11
   ```

### cat 和 EOF

```
cat：该文本输出命令用于显示文本的全部内容，并全部打印输出
EOF：文本结束符，即 ```end of file```，表示文件内容的结束
```

- ```cat > FileName << EOF```：覆盖写入
   ```bash
   # echo aa > 1.log
   
   # cat 1.log
   aa
   ```
   
   编辑 1.sh:
  
   ```bash
   #!/bin/sh
   
   cat > 1.log << EOF
   11
   EOF
   ```
   
   ```bash
   # ./1.sh
   
   # cat 1.log
   11
   ```

- ```cat >> FileName << EOF```：追加写入
   ```bash
   # echo aa > 1.log
   
   # cat 1.log
   aa
   ```
   
   编辑 1.sh:
  
   ```bash
   #!/bin/sh
   
   cat >> 1.log << EOF
   11
   EOF
   ```
   
   ```bash
   # ./1.sh
   
   # cat 1.log
   aa
   11
   ```

- ```cat > FileName```：覆盖写入，使用 ```Ctrl + C``` 或者 ```Ctrl + D``` 退出编辑
