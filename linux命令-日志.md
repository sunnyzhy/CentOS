# linux 命令-日志

- ```/var/log/message```: 系统启动后的信息和错误日志，是 Red Hat Linux 中最常用的日志之一
- ```/var/log/secure```: 与安全相关的日志信息
- ```/var/log/maillog```: 与邮件相关的日志信息
- ```/var/log/cron```: 与定时任务相关的日志信息
- ```/var/log/spooler```: 与 UUCP 和 news 设备相关的日志信息
- ```/var/log/boot.log```: 守护进程启动和停止相关的日志消息
- ```/var/log/wtmp```: 该日志文件永久记录每个用户登录、注销及系统的启动、停机的事件

如实时查看系统日志： ```tail -f /var/log/messages```
