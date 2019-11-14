# 查看端口
## lsof -i:端口号
```
# lsof -i:8080
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    2103 root   17u  IPv4  28338      0t0  TCP *:webcache (LISTEN)
```

## netstat -tunlp | grep 端口号
```
# netstat -tunlp | grep 8080
tcp        0      0 0.0.0.0:8080            0.0.0.0:*               LISTEN      2103/java
```

# 通过PID查看进程完整信息
## netstat -anp | grep PID
```
# netstat -anp | grep 2103
tcp        0      0 0.0.0.0:8080            0.0.0.0:*               LISTEN      2103/java           
unix  2      [ ]         STREAM     CONNECTED     28339    2103/java            
unix  2      [ ]         STREAM     CONNECTED     28594    2103/java
```

## ps -ef | grep PID
```
# ps -ef | grep 2103
root      2103     1  0  2018 ?        11:17:09 java -jar -Xms64M -Xmx128M -Xmn20M rocketmq-console-ng-1.0.0.jar
root     13057 11227  0 16:34 pts/2    00:00:00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn 2103
```

# 查看java的执行路径
```
# which java
/usr/bin/java
```

# 查看JDK的安装路径
```
# ls -lrt /usr/bin/java
lrwxrwxrwx. 1 root root 22 5?. 15 11:49 /usr/bin/java -> /etc/alternatives/java

# ls -lrt /etc/alternatives/java
lrwxrwxrwx. 1 root root 41 5?. 15 11:49 /etc/alternatives/java -> /usr/java/jdk1.8.0_202-amd64/jre/bin/java

# cd /usr/java/jdk1.8.0_202-amd64

# ls
bin             jre      README.html                         THIRDPARTYLICENSEREADME.txt
COPYRIGHT       lib      release
include         LICENSE  src.zip
javafx-src.zip  man      THIRDPARTYLICENSEREADME-JAVAFX.txt
```

# 查看当前所在目录
```
# cd /usr/local

# pwd
/usr/local
```

# 查看磁盘空间
## 查看系统磁盘空间大小
```
# df -h
Filesystem               Size  Used Avail Use% Mounted on
/dev/mapper/centos-root   48G   37G   12G  77% /
devtmpfs                 7.8G     0  7.8G   0% /dev
tmpfs                    7.8G   14M  7.8G   1% /dev/shm
tmpfs                    7.8G  744M  7.1G  10% /run
tmpfs                    7.8G     0  7.8G   0% /sys/fs/cgroup
/dev/sda1               1014M  178M  837M  18% /boot
/dev/mapper/centos-home   24G   13G   11G  53% /home
tmpfs                    1.6G   16K  1.6G   1% /run/user/42
tmpfs                    1.6G     0  1.6G   0% /run/user/1000
tmpfs                    1.6G     0  1.6G   0% /run/user/0
```

## 查看当前目录下的所有文件大小
```
# du -sh
118M	.
```

## 查看指定目录下的所有文件大小
```
# du -h /usr/local/
```

## 查看指定文件大小
```
# du -h access.log
7.7M	access.log
```

## 查指定目录大小
```
# du -sh /usr/local
118M	/usr/local
```

# 切换账号
- root 切换到普通用户

```
# su zhy

$ 
```
由 root 切换到 zhy 之后，# 号变成了 $

- 普通用户切换到 root

```
$ su root
Password: 

# 
```
由普通用户切换到 root 之后，$ 号变成了 #

# 查看文件权限
```
# ls -l /usr/local/redis
```

# 修改文件的所有者
```
# chown zhy: redis-start.sh
```
root 账号才能修改文件的所有者

# 修改jar里的application.properties
1. 用 vim xxx.jar，显示jar包内的文件列表

```
# vim xxx.jar
```

2. 输入 /application ，定位到对应的application.properties文件

3. 按 Enter 键，之后就可以进行编辑了
