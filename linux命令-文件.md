# 创建文件目录
```bash
# mkdir zz
```

# 查看目录下文件
```bash
# ls

# ls -a // 显示所有文件及目录

# ls -l // 显示文件名、权限、拥有者、文件大小等
```

# 复制文件
```bash
# cp /home/run.sh /usr/local
```

# 修改文件名
```bash
# mv /home/run.sh /home/1.sh
```

# 修改文件夹名
```bash
# mv /home/zz /home/z
```

# 移动文件
```bash
# mv /root/run.sh /usr/local
```

# 移动文件夹
```bash
# mv /home/z /usr/local
```

# 查看当前所在目录
```bash
# cd /usr/local

# pwd
/usr/local
```

# 查看登录用户信息
```bash
# who
root     pts/0        2020-06-10 10:16 (xx-pc)
```

# 显示文件全部内容
```bash
# cat nohup.out
```

# 动态显示文件的内容
```bash
# tail -f -n 30 nohup.out
```

- -f：循环读取
- -n <行数>：显示文件的尾部 n 行内容

# 显示文件前 n 行内容
```bash
# head -n 10 nohup.out
```

# 删除文件
```bash
# rm -rf zz
```

- -r或-R：递归处理，将指定目录下的所有文件与子目录一并处理
- -f：强制删除文件或目录

# 清空文件内容
## 第一种
```bash
# > nohup.out
```

## 第二种
```bash
# echo "" > nohup.out
```

## 第三种
```bash
# cat /dev/null > nohup.out
```

# 服务器之间传输文件
```bash
# scp -r /usr/local/dir target_username@target_ip:/usr/local/dir
target_username@target_ip's password:
```

# 压缩/解压文件
## tar.gz
### 压缩
```bash
# tar -czvf xxx.tar.gz(目标文件) 源文件
```

### 解压
```bash
# tar -xzvf xxx.tar.gz -C dir
```

## jar
### 压缩
```bash
# cd xxx

# jar -cvf0m xxx.jar ./META-INF/MANIFEST.MF .
```

### 解压
```bash
# unzip xxx.jar -d xxx
```
