# 创建文件目录
```
# mkdir zz
```

# 查看目录下文件
```
# ls

# ls -a // 显示所有文件及目录

# ls -l // 显示文件名、权限、拥有者、文件大小等
```

# 复制文件
```
# cp /home/run.sh /usr/local
```

# 修改文件名
```
# mv /home/run.sh /home/1.sh
```

# 修改文件夹名
```
# mv /home/zz /home/z
```

# 移动文件
```
# mv /root/run.sh /usr/local
```

# 移动文件夹
```
# mv /home/z /usr/local
```

# 查看当前所在目录
```
# cd /usr/local

# pwd
/usr/local
```

# 查看登录用户信息
```
# who
root     pts/0        2020-06-10 10:16 (xx-pc)
```

# 显示文件全部内容
```
# cat nohup.out
```

# 动态显示文件的内容
```
# tail -f -n 30 nohup.out
```

- -f：循环读取
- -n <行数>：显示文件的尾部 n 行内容

# 显示文件前 n 行内容
```
# head -n 10 nohup.out
```

# 删除文件
```
# rm -rf zz
```

- -r或-R：递归处理，将指定目录下的所有文件与子目录一并处理
- -f：强制删除文件或目录

# 清空文件内容
## 第一种
```
# > nohup.out
```

## 第二种
```
# echo "" > nohup.out
```

## 第三种
```
# cat /dev/null > nohup.out
```
