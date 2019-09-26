# 关闭VMware的DHCP
1. 打开VMware的 编辑 -> 虚拟网络编辑器 -> 选择VMnet8 -> 不勾选“使用本地DHCP服务将IP地址分配给虚拟机”

2. 打开NAT设置，查看网关IP，如192.168.253.2

3. 打开VMware的 虚拟机 -> 设置 -> 网络适配器 -> NAT模式

# 设置静态IP
```
# cd /etc/sysconfig/network-scripts

# vim ifcfg-eno16777736
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.253.107
BROADCAST=192.168.253.255
GATEWAY=192.168.253.2
NETMASK=255.255.255.0
IPV6INIT=yes
ARPCHECK=no
DNS1=8.8.8.8

# systemctl restart network
```

# ifconfig 只有 lo 和 virbr0
# 重启出错（code=exited, status=1/FAILURE）
```
# systemctl stop NetworkManager
```
