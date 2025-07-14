# SIOCSIFFLAGS: Operation Not Possible Due to RF Kill


### 问题描述

报错信息：SIOCSIFFLAGS: Operation not possible due to RF-kill

我想让一块无线网卡up起来，结果没想到报错了
```sh
[root@localhost opt]# ifconfig wls35u1 up
SIOCSIFFLAGS: Operation not possible due to RF-kill
```
查了一下，RF-KILL是一个打开和关闭无线设备的工具。 所以这是一打开无线设备（wifi）的错误。

### 解决办法

1. 查看所有无线设备当前状态
```sh
[root@localhost opt]# rfkill list all
2: phy2: Wireless LAN
	Soft blocked: yes
	Hard blocked: no

# 可以看出Hard blocked和 software blocked之间的同步失败
```

2. 解锁设备
```sh
# 解锁所有wifi设备
[root@localhost opt]# rfkill unblock all
# 再次查看状态
[root@localhost opt]# rfkill list all
2: phy2: Wireless LAN
	Soft blocked: no
	Hard blocked: no
```
此刻，可以使用`ifconfig`来启动wifi网卡了。


---

> : 蓝红柿  
> URL: http://localhost:1313/zh/zh/posts/operation-not-possible-due-to-rf-kill/  

