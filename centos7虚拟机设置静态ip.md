# centos7 虚拟机设置静态 ip

## NAT 模式

## 关闭VMware的DHCP

1. 打开 VMware 的 ```编辑 -> 虚拟网络编辑器 -> 选择VMnet8(NAT模式) -> 不勾选"使用本地DHCP服务将IP地址分配给虚拟机"```

2. 打开 NAT 设置，查看网关 IP，如 192.168.253.2

3. 打开 VMware 的 ```虚拟机 -> 设置 -> 网络适配器 -> NAT模式```

## 设置静态IP

```bash
# cd /etc/sysconfig/network-scripts

# vim ifcfg-eno16777736
BOOTPROTO=static
ONBOOT=yes
IPV6INIT=yes
ARPCHECK=no
IPADDR=192.168.253.107
BROADCAST=192.168.253.255
GATEWAY=192.168.253.2
NETMASK=255.255.255.0
DNS1=8.8.8.8

# systemctl restart network
```

## Bridged 模式

## 配置 Bridged 模式

1. 打开VMware的 ```编辑 -> 虚拟网络编辑器 -> 选择VMnet0(桥接模式)```

## 设置静态IP

查看宿主机的网络信息:

```bash
以太网适配器 以太网:

   连接特定的 DNS 后缀 . . . . . . . : 
   本地链接 IPv6 地址. . . . . . . . : fe80::41f:b65d:3b35:8f67%9
   IPv4 地址 . . . . . . . . . . . . : 192.168.0.100
   子网掩码  . . . . . . . . . . . . : 255.255.255.0
   默认网关. . . . . . . . . . . . . : 192.168.0.1
```

修改虚拟系统的网络信息:

```bash
# cd /etc/sysconfig/network-scripts

# vim ifcfg-eno16777736
BOOTPROTO=static
ONBOOT=yes
IPV6INIT=yes
ARPCHECK=no
IPADDR=192.168.0.107
GATEWAY=192.168.0.1
NETMASK=255.255.255.0
DNS1=8.8.8.4

# systemctl restart network
```

## FAQ

### ifconfig 只有 lo 和 virbr0

1. 用 ifconfig 查看

```bash
# ifconfig
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 320  bytes 25920 (25.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 320  bytes 25920 (25.3 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:cd:d6:7f  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

2. 用 ip addr 查看

```bash
# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN qlen 1000
    link/ether 00:50:56:39:87:0a brd ff:ff:ff:ff:ff:ff
3: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN 
    link/ether 52:54:00:cd:d6:7f brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0
       valid_lft forever preferred_lft forever
4: virbr0-nic: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast master virbr0 state DOWN qlen 500
    link/ether 52:54:00:cd:d6:7f brd ff:ff:ff:ff:ff:ff
```

3. 查看 network-scripts

```bash
# cd /etc/sysconfig/network-scripts
```

如果有 ifcfg-eno16777736 却没有 ifcfg-ens33，就修改 ifcfg-eno16777736

```bash
# vim ifcfg-eno16777736
NAME=ens33
DEVICE=ens33

# mv ifcfg-eno16777736 ifcfg-ens33
```

4. 重启 network

```bash
# systemctl restart network
```

### 重启 network 出错（code=exited, status=1/FAILURE）

```bash
# systemctl stop NetworkManager 临时关闭

# systemctl disable NetworkManager 永久关闭网络管理命令

# systemctl restart network
```
