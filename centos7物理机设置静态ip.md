# 配置 network
```
# vim /etc/sysconfig/network
NETWORKING=yes
```

# 配置静态 IP
```
# vim /etc/sysconfig/network-scripts/ifcfg-enp4s0
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
IPADDR=192.168.0.107
NETMASK=255.255.255.0
GATEWAY=192.168.0.1
DNS1=8.8.8.8
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp4s0
UUID=fdb55853-4f3d-4d71-8d38-acf036939942
DEVICE=enp4s0
ONBOOT=yes

# systemctl restart network
```
