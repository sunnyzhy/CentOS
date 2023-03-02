# Crontab 定时任务

## cron 介绍

crontab 命令是 cron table 的简写，它是 cron 的配置文件，也可以称为定时任务列表，存在于以下目录:

- ```/var/spool/cron/```: 这个目录存放的是每个用户（比如: root）的 crontab 任务，如果是 root 用户登录的，那么使用 ```crontab -e``` 等价于 ```vim /var/spool/cron/root```
- ```/etc/crontab```: 这个文件负责调度各种管理和维护任务
- ```/etc/cron.d/```: 这个目录用来存放任何要执行的 crontab 文件或脚本
- ```/etc/cron.hourly/```: 这个目录用来存放 ***每小时*** 执行一次的任务
- ```/etc/cron.daily/```: 这个目录用来存放 ***每天*** 执行一次的任务
- ```/etc/cron.weekly/```: 这个目录用来存放 ***每星期*** 执行一次的任务
- ```/etc/cron.monthly/```: 这个目录用来存放 ***每月*** 执行一次的任务

## cron 语法

```bash
crontab [-u username]　　　　//省略用户表表示操作当前用户的 crontab
    -e      (编辑工作表)
    -l      (列出工作表里的命令)
    -r      (删除工作作)
```

定时任务的构成为 ```时间 + 动作```:

- 时间部分的格式为 ```分 小时 日 月 星期```
   - ```*```: 取值范围内的所有数字，注: ```0``` 表示在整时、整分
   - ```/```: 每，比如每分钟、每小时等
   - ```-```: 从 X 到 Z
   - ```,```: 散列数字
- 动作一般为 shell 脚本文件

## 实例

- 每分钟执行一次 command
   ```bash
   * * * * * command
   ```
- 每小时执行一次 command，***分钟位配置为 ```0```***
   ```bash
   0 */1 * * * command
   ```
- 每小时的第 3 和第 15 分钟执行
   ```bash
   3,15 * * * * command
   ```
- 在上午 ```8:00``` 到 ```11:00``` 的第 3 和第 15 分钟执行
   ```bash
   3,15 8-11 * * * command
   ```
- 每隔两天的上午 ```8:00``` 到 ```11:00``` 的第 3 和第 15 分钟执行
   ```bash
   3,15 8-11 */2  *  * command
   ```
- 每周一上午 ```8:00``` 到 ```11:00``` 的第 3 和第 15 分钟执行
   ```bash
   3,15 8-11 * * 1 command
   ```
- 每晚的 ```21:30``` 重启 smb
   ```bash
   30 21 * * * /etc/init.d/smb restart
   ```
- 每月 ```1、10、22``` 日的 ```4:45``` 重启 smb
   ```bash
   45 4 1,10,22 * * /etc/init.d/smb restart
   ```
- 每周六、周日的 ```1:10``` 重启 smb
   ```bash
   10 1 * * 6,0 /etc/init.d/smb restart
   ```
- 每天 ```18:00``` 至 ```23:00``` 之间每隔 30 分钟重启 smb
   ```bash
   0,30 18-23 * * * /etc/init.d/smb restart
   ```
- 每星期六的晚上 ```11:00 PM``` 重启 smb
   ```bash
   0 23 * * 6 /etc/init.d/smb restart
   ```
- 每小时重启 smb
   ```bash
   0 */1 * * * /etc/init.d/smb restart
   ```
- 晚上 ```11:00``` 到早上 ```7:00``` 之间，每隔一小时重启 smb
   ```bash
   0 23-7/1 * * * /etc/init.d/smb restart
   ```
