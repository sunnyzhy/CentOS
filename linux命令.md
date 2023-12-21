# linux命令

## 查看端口

### lsof -i:端口号

```bash
# lsof -i:8080
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    2103 root   17u  IPv4  28338      0t0  TCP *:webcache (LISTEN)
```

### netstat -tunlp | grep 端口号

```bash
# netstat -tunlp | grep 8080
tcp        0      0 0.0.0.0:8080            0.0.0.0:*               LISTEN      2103/java
```

## 通过PID查看进程完整信息

### netstat -anp | grep PID

```bash
# netstat -anp | grep 2103
tcp        0      0 0.0.0.0:8080            0.0.0.0:*               LISTEN      2103/java           
unix  2      [ ]         STREAM     CONNECTED     28339    2103/java            
unix  2      [ ]         STREAM     CONNECTED     28594    2103/java
```

### ps -ef | grep PID

```bash
# ps -ef | grep 2103
root      2103     1  0  2018 ?        11:17:09 java -jar -Xms64M -Xmx128M -Xmn20M rocketmq-console-ng-1.0.0.jar
root     13057 11227  0 16:34 pts/2    00:00:00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn 2103
```

## 根据PID查看进程的绝对路径

```bash
# ps -ef | grep service_name

# cd /proc/pid

# ls -l
```

## 查看java的执行路径

```bash
# which java
/usr/bin/java
```

## 查看JDK的安装路径

```bash
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

## 查看当前所在目录

```bash
# cd /usr/local

# pwd
/usr/local
```

## 查看磁盘空间

### 查看系统磁盘空间大小

```bash
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

### 查看当前目录下的所有文件大小

```bash
# du -sh
118M	.
```

### 查看指定目录下的所有文件大小

```bash
# du -h /usr/local/
```

### 查看指定文件大小

```bash
# du -h access.log
7.7M	access.log
```

### 查指定目录大小

```bash
# du -sh /usr/local
118M	/usr/local
```

### 查找已删除但未释放的文件

```bash
# lsof -n | grep deleted

# kill -9 pid
```

注意：

使用 rm 删除文件的时候，如果有进程打开了这个文件，却没有关闭这个文件的句柄，那么linux内核还是不会释放这个文件的磁盘空间。可以 echo > filename 清空文件。

## 切换账号

- root 切换到普通用户

   ```bash
   # su zhy
   
   $ 
   ```
   由 root 切换到 zhy 之后，# 号变成了 $

- 普通用户切换到 root

   ```bash
   $ su root
   Password: 
   
   # 
   ```

   或者

   ```bash
   $ sudo su
   ```

   由普通用户切换到 root 之后，$ 号变成了 #

## 修改密码

```bash
passwd <username>
```

## 远程登录

```bash
ssh <username>@<target_server_ip>
```

## 查看文件权限

```bash
# ls -l /usr/local/redis
```

## 修改文件的所有者

```bash
# chown zhy: redis-start.sh
```
root 账号才能修改文件的所有者

## 远程传输文件

```bash
scp -r <source_dir> <remote_server_username>@<remote_server_ip>:<remote_server_dir>
```

## 修改jar里的application.properties

1. 用 vim xxx.jar，显示jar包内的文件列表

```bash
# vim xxx.jar
```

2. 输入 /application ，定位到对应的application.properties文件

3. 按 Enter 键，之后就可以进行编辑了

## 系统时区

### 查看系统时间

```bash
# date
```

### 查看系统当前时区

```bash
# timedatectl
```

### 查看系统所有时区

```bash
# timedatectl list-timezones
```

### 设置系统时区

```bash
# timedatectl set-timezone Asia/Shanghai
```

## 校准服务器时间
```bash
# ntpdate 1.cn.pool.ntp.org

# hwclock -w

# date
```

## 查看 Linux 版本信息

### 查看版本号

```bash
# ll /etc/*centos*
-rw-r--r--. 1 root root 37 Nov 23  2020 /etc/centos-release
-rw-r--r--. 1 root root 51 Nov 23  2020 /etc/centos-release-upstream

# cat /etc/centos-release
CentOS Linux release 7.9.2009 (Core)
```

### 查看内核版本

```bash
# uname -r
3.10.0-1127.el7.x86_64
```

### 查看系统架构

```bash
# uname -m
x86_64

# arch
x86_64
```

- ```x86_64```: ```X86``` 架构；``X86``` 使用复杂指令集(CISC)，广泛应用于 PC 和服务器领域；用于设计高性能的处理器。
- ```aarch64```:  ```ARM``` 架构；```ARM``` 使用精简指令集(RISC)，广泛应用于移动端和嵌入式领域；用于设计低功耗的处理器。

### 查看操作系统位数

```bash
# getconf LONG_BIT
64
```

### 查看 cpu 信息

```bash
lscpu
```

### 查看 cpu 核数

- ```nproc```
- ```lscpu | grep "CPU(s)"``` 命令
- 先输入 ```top``` 命令，再按 ```1```

### 判断服务器的虚拟机类型

```bash
systemd-detect-virt
```

- 物理机：```none```
- 虚拟机
   |ID|Product|
   |--|--|
   |qemu|QEMU 软件虚拟机(未使用KVM)|
   |kvm|Linux 内核虚拟机(使用除 Oracle Virtualbox 之外的其他虚拟机管理程序)|
   |zvm|s390 z/VM|
   |vmware|VMware 虚拟机|
   |microsoft|Hyper-V 虚拟机|
   |oracle|Oracle VirtualBox 虚拟机|
   |xen|Xen 虚拟机(仅 domU, 非 dom0)|
   |bochs|Bochs 模拟器|
   |uml|User-mode Linux|
   |parallels|Parallels Desktop, Parallels Server|
   |bhyve|bhyve, FreeBSD hypervisor|
   |qnx|QNX hypervisor|

- 容器
   |ID|Product|
   |--|--|
   |openvz|OpenVZ/Virtuozzo|
   |lxc|LXC 容器|
   |lxc-libvirt|通过 libvirt 实现的容器|
   |systemd-nspawn|systemd 最简容器)
   |docker|Docker 容器|
   |rkt|rkt 应用容器|

## 设置开机启动脚本

***把 .sh 脚本加入 ```/etc/rc.local```***

```bash
# vim /etc/rc.local
/usr/autostart/nginx.sh &
```

## 创建定时任务

```bash
# crontab -l

# crontab -e
# 每天凌晨两点，自动从 192.168.5.10 同步一次
0 2 * * * ntpdate 192.168.5.10
```

### FAQ

```bash
# crontab -l
no crontab for root
```

解决方法: 同样在 ```root``` 用户下输入 ```crontab -e```, 按 ```Esc```, 再按```:wq```, 最后回车。
