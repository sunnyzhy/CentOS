NAT模式主机ping不通虚拟机，最大的原因可能是VMware Network Adapter VMnet8网络适配器IP与虚拟机IP不在同一个网段。

# windows主机
```
> ipconfig
以太网适配器 VMware Network Adapter VMnet8:

   连接特定的 DNS 后缀 . . . . . . . :
   本地链接 IPv6 地址. . . . . . . . : fe80::3d36:ecc0:6bdd:b6ff%21
   自动配置 IPv4 地址  . . . . . . . : 169.254.182.255
   子网掩码  . . . . . . . . . . . . : 255.255.0.0
   默认网关. . . . . . . . . . . . . :
```
VMware Network Adapter VMnet8的IP、子网掩码和默认网关为：
IP:192.168.1.25
子网掩码:255.255.0.0
默认网关:

# linux虚拟机
```
# ifconfig
eno16777736: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.253.107  netmask 255.255.255.0  broadcast 192.168.253.255
        inet6 fe80::20c:29ff:fe37:38c8  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:37:38:c8  txqueuelen 1000  (Ethernet)
        RX packets 4842  bytes 1742768 (1.6 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 3667  bytes 621931 (607.3 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         192.168.253.2   0.0.0.0         UG    100    0        0 eno16777736
192.168.122.0   0.0.0.0         255.255.255.0   U     0      0        0 virbr0
192.168.253.0   0.0.0.0         255.255.255.0   U     100    0        0 eno16777736
```
虚拟机的IP、子网掩码和默认网关为:
IP:192.168.253.107
子网掩码:255.255.255.0
默认网关:192.168.253.2

# 解决方法
修改VMware Network Adapter VMnet8配置:
IP:192.168.253.1
子网掩码:255.255.255.0
默认网关:192.168.253.2
