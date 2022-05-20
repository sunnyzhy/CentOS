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
### 第一种
```bash
# > nohup.out
```

### 第二种
```bash
# echo "" > nohup.out
```

### 第三种
```bash
# cat /dev/null > nohup.out
```

## 服务器之间传输文件
### 传输单个文件
```bash
# scp -r /usr/local/dir target_username@target_ip:/usr/local/dir
target_username@target_ip's password:
```

### 传输指定目录下的所有文件
```bash
# scp -r /usr/local/dir/* target_username@target_ip:/usr/local/dir
target_username@target_ip's password:
```

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

***后续完善 sed 指令***

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
