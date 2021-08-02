# adb shell 命令获取IP、网关等信息

通过shell命令设置（获取）IP、网关、dns信息，需要获取root权限

## 查看所有网络信息

    C:\>adb shell
    root@android:/ # netcfg
    netcfg
    ip6tnl0  DOWN             0.0.0.0/0   0x00000080 00:00:00:00:00:00
    gre0     DOWN             0.0.0.0/0   0x00000080 00:00:00:00:00:00
    eth0     UP         192.168.0.180/24  0x00001043 00:00:00:ec:0a:00
    sit0     DOWN             0.0.0.0/0   0x00000080 00:00:00:00:00:00
    lo       UP             127.0.0.1/8   0x00000049 00:00:00:00:00:00
    tunl0    DOWN             0.0.0.0/0   0x00000080 00:00:00:00:00:00

## 查看 eth0

    root@android:/ # ifconfig eth0
    ifconfig eth0
    eth0: ip 192.168.0.180 mask 255.255.255.0 flags [up broadcast running multicast]

## 查看 dns

    root@android:/ # getprop net.eth0.dns1
    getprop net.eth0.dns1
    8.8.8.8
    root@android:/ # getprop net.eth0.dns2
    getprop net.eth0.dns2
    8.8.4.4

## 设置 ip

    root@android:/ # ifconfig eth0 192.168.0.173 netmask 255.255.255.0
    ifconfig eth0 192.168.0.173 netmask 255.255.255.0
    root@android:/ # ifconfig eth0
    ifconfig eth0
    eth0: ip 192.168.0.173 mask 255.255.255.0 flags [up broadcast running multicast]

## 设置网关 Gateway

    root@android:/ # route add default gw 192.168.0.1 dev eth0
    route add default gw 192.168.0.1 dev eth0

## 添加 dns

    root@android:/ # setprop net.eth0.dns1 8.8.8.8
    setprop net.eth0.dns1 8.8.8.8
    root@android:/ # setprop net.eth0.dns2 8.8.4.4
    setprop net.eth0.dns2 8.8.4.4

## 查看 eth 配置信息

    root@android:/ # getprop | grep eth0
    getprop | grep eth0
    [dhcp.eth0.dns1]: [192.168.0.1]
    [dhcp.eth0.dns2]: []
    [dhcp.eth0.dns3]: []
    [dhcp.eth0.dns4]: []
    [dhcp.eth0.gateway]: [192.168.0.1]
    [dhcp.eth0.ipaddress]: [192.168.0.180]
    [dhcp.eth0.leasetime]: [3600]
    [dhcp.eth0.mask]: [255.255.255.0]
    [dhcp.eth0.pid]: [13800]
    [dhcp.eth0.reason]: [PREINIT]
    [dhcp.eth0.result]: [failed]
    [dhcp.eth0.server]: [192.168.0.1]
    [dhcp.eth0.vendorInfo]: []
    [net.change]: [net.eth0.dns2]
    [net.eth0.dns1]: [8.8.8.8]

[原文链接](https://blog.csdn.net/Liuqz2009/article/details/52094154)
