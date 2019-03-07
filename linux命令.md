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
