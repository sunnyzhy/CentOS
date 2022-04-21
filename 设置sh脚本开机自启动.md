# 设置 sh 脚本开机自启动

## 创建测试脚本

```bash
# vim /home/test.sh
#!/bin/bash
nohup java -jar -XX:+HeapDumpOnOutOfMemoryError -Xmx256m -Xms256m /usr/local/test.jar > /dev/null 2>&1 &
```

## 设置开机自启动

把 ```test.sh``` 添加到 ```/etc/rc.d/rc.local``` 文件的末尾:

```bash
# vim /etc/rc.d/rc.local
/home/test.sh
```

## 添加执行权限

```bash
# chmod +x /home/test.sh
# chmod +x /etc/rc.d/rc.local
```
