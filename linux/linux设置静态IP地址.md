linux 设置静态IP地址
===============================

+ 首页要知道静态的IP地址的 IP,子网掩码,网关


```
[root@localhost ~]# vim /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
HWADDR=1C:1B:0D:06:0D:81
TYPE=Ethernet
UUID=167a991b-96c6-4405-9914-120860bfb61b
ONBOOT=yes
NM_CONTROLLED=yes
#BOOTPROTO=dhcp
BOOTPROTO=static 必要
IPADDR=192.168.5.10 必要
NETMASK=255.255.255.0 必要
NETWORK=192.168.5.0 不必要
GATEWAY=192.168.5.1 必要 / 不设置无法上网 局域网可以使用
BROADCAST=192.168.5.255  不必要


[root@localhost ~]# vim /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=localhost.localdomain
NETWORKING_IPV6=no
#GATEWAY=192.168.5.1 可以不设置
```