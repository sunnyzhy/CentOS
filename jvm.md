# jvm

## jstack

### 使用方法

1. 通过 ```top``` 命令查找占用 cpu 资源最多的进程
   ```
   # atop
    1581  0.00s  0.54s      0K   204K      0K  2088K  root     root      --   -   171 S	  0   5% java
   ```

2. 通过 ```jstack``` 查看当前 java 进程的堆栈信息
   ```
   # jstack 1581
   ```

3. 把当前 java 进程的堆栈信息输出到文件
   ```
   # jstack 1581 > /usr/local/jstack/dump.log
   ```

4. 通过 ```top -Hp 1581``` 查看该进程下各个线程的 cpu 使用情况
   ```
   # top -Hp 1581
     PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                     
    3504 root      20   0   14.2g   4.7g   3.5g S  1.3 15.1 419:09.92 java                                        
    3605 root      20   0   14.2g   4.7g   3.5g S  1.3 15.1 308:33.04 java                                        
    3617 root      20   0   14.2g   4.7g   3.5g S  1.0 15.1 245:09.55 java                                        
    3528 root      20   0   14.2g   4.7g   3.5g S  0.7 15.1  55:44.43 java                                        
    3596 root      20   0   14.2g   4.7g   3.5g S  0.7 15.1 126:38.19 java                                        
    3831 root      20   0   14.2g   4.7g   3.5g S  0.7 15.1  14:33.29 java                                        
    3512 root      20   0   14.2g   4.7g   3.5g S  0.3 15.1  44:39.93 java 
   ```

5. 通过 ```jstack``` 查看占用 cpu 资源最多的线程的堆栈信息
   ```
   # jstack 3504
   ```

6. 把线程的堆栈信息输出到文件
   ```
   # jstack 3504 > /usr/local/jstack/dump.log
   ```

### 堆栈信息分析

```
Full thread dump Java HotSpot(TM) 64-Bit Server VM (25.151-b12 mixed mode):

"Attach Listener" #187 daemon prio=9 os_prio=0 tid=0x00007f8cb4004620 nid=0xdb0 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"ClientManageThread_10" #174 prio=5 os_prio=0 tid=0x00007f8cf8029c20 nid=0xe15 waiting on condition [0x00007f8a10179000]
   java.lang.Thread.State: WAITING (parking)
	at sun.misc.Unsafe.park(Native Method)
	- parking to wait for  <0x00000000c010f1f0> (a java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject)
	at java.util.concurrent.locks.LockSupport.park(LockSupport.java:175)
	at java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject.await(AbstractQueuedSynchronizer.java:2039)
	at java.util.concurrent.LinkedBlockingQueue.take(LinkedBlockingQueue.java:442)
	at java.util.concurrent.ThreadPoolExecutor.getTask(ThreadPoolExecutor.java:1074)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1134)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
```

说明:

- 堆栈信息里每一个线程都有一个 nid，对应线程 pid 的 16 进制的值。可以用 ```printf "%x" xxxx``` 把 10 进制转换为 16 进制。
- 堆栈信息里的线程状态:
   - RUNNABLE: 线程处于执行中
   - BLOCKED: 线程被阻塞
   - WATING: 线程无期限等待
   - TIMED_WATING: 处于 waiting 状态，但设置的有超时时间
