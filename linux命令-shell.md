# linux命令-shell

# 查找 jar 进程 ID，并杀死进程

假如 jar 文件都是以 ```st-``` 开头。

```bash
#!/bin/sh

PID=$(ps -ef | grep st- | grep -v grep | awk '{print $2}')
echo $PID
echo "---------------"

for pid in $PID
do
  #kill -9 $pid
  echo "killed $pid"
done
echo "---------------"
```
