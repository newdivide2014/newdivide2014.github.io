# 华为交换机一些命令及回显信息

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1460966070&auto=1&height=66"></iframe>


1. 显示版本信息
```sh
display version
Huawei Versatile Routing Platform Software
VRP (R) software, Version 5.110 (S5700 V200R001C00SPC300)
Copyright (C) 2000-2012 HUAWEI TECH CO., LTD
Quidway S5700-24TP-SI-AC Routing Switch uptime is 0 week, 0 day, 0 hour, 10 minutes

CX22EFGEA 0(Master) : uptime is 0 week, 0 day, 0 hour, 10 minutes
256M bytes DDR Memory
32M bytes FLASH
Pcb      Version :  VER B
Basic  BOOTROM  Version :  162 Compiled at May 31 2012, 10:56:32
CPLD   Version : 5 
Software Version : VRP (R) Software, Version 5.110 (V200R001C00SPC300)
```

2. 显示当前配置
```sh
<Quidway>display current-configuration configuration user-interface
#
user-interface con 0
 authentication-mode password
 set authentication password cipher %$%$1V2:B|!|f%HSgrWXjj*W,e\Sbo{|Km6oOGipQwSRK|VI#kb]%$%$
user-interface vty 0 4
user-interface vty 16 20
#
return
```

3. 显示ssh服务状态
```sh
<Quidway>display ssh server status 
 SSH version                         :1.99
 SSH connection timeout              :60 seconds
 SSH server key generating interval  :0 hours
 SSH authentication retries          :3 times
 SFTP server                         :Disable
 Stelnet server                      :Disable
 Scp server                          :Disable

```

4. 显示snmp状态
```sh
<Quidway>display snmp-agent statistics
Error: SNMP agent is not enabled.

```

5. 显示telnet服务状态
```sh
<Quidway>display telnet server status
 TELNET IPv4 server                       :Enable
 TELNET IPv6 server                       :Enable
 TELNET server port                       :23
```

6. 显示设备状态
```sh
<Quidway>display device 
S5700-24TP-SI-AC's Device status:
Slot  Sub  Type         Online    Power      Register       Status     Role  
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
0     -    5724TP       Present   PowerOn    Registered     Normal     Master
```

7. 显示环境(好像显示的是温度)
```sh
<Quidway>display environment 
Environment information:
Temperature information:
SlotID   CurrentTemperature  LowLimit  HighLimit
             (deg c )        (deg c)   (deg c )        
 0              41             0         92              
```

8. 显示ftp、http服务状态
```sh
<Quidway>display ftp-server 
Info: The FTP server is already disabled.

<Quidway>display http server
   HTTP Server Status              : disabled
   HTTP Server Port                : 80(80)
   HTTP Timeout Interval           : 20
   Current Online Users            : 0
   Maximum Users Allowed           : 5
   HTTP Secure-server Status       : disabled
   HTTP Secure-server Port         : 443(443)
   HTTP SSL Policy                 : 
```

9. 显示icmp状态
```sh
<Quidway>display icmp statistics 
  Input: bad formats            0      bad checksum                     0
         echo                   0      destination unreachable          0
         source quench          0      redirects                        0
         echo reply             0      parameter problem                0
         timestamp              0      information request              0
         mask requests          0      mask replies                     0
         time exceeded          0
         Mping request          0      Mping reply                      0
  Output:echo                   0      destination unreachable          0
         source quench          0      redirects                        0
         echo reply             0      parameter problem                0
         timestamp              0      information reply                0
         mask requests          0      mask replies                     0
         time exceeded          0
         Mping request          0      Mping reply                      0
```

10. 显示本地用户
```sh
<Quidway>display local-user 
  ----------------------------------------------------------------------------
  User-name                      State  AuthMask  AdminLevel  
  ----------------------------------------------------------------------------
  admin                          A      H         -          
  ----------------------------------------------------------------------------
  Total 1 user(s)
```

11. 显示ntp服务状态
```sh
<Quidway>display ntp-service status
 clock status: unsynchronized 
 clock stratum: 16 
 reference clock ID: none
 nominal frequency: 60.0002 Hz 
 actual frequency: 60.0002 Hz 
 clock precision: 2^17
 clock offset: 0.0000 ms 
 root delay: 0.00 ms 
 root dispersion: 0.00 ms 
 peer dispersion: 0.00 ms 
 reference time: 00:00:00.000 UTC Jan 1 1900(00000000.00000000)
```

12. 显示radius服务授权配置和显示radius服务配置
```sh
<Quidway>display radius-server authorization configuration 

 0 Radius authorization server(s) in total

<Quidway>display radius-server configuration 
  Total of radius template :0 
```

13. 显示ssl策略
```sh
<Quidway>display ssl policy 
Error: No policy exists.
```

14. 显示tcp状态
```sh
<Quidway>display tcp status
TCPCB    Tid/Soid Local Add:port        Foreign Add:port      VPNID  State
0d4315d0 102/1    0.0.0.0:23            0.0.0.0:0             -1     Listening

```

---

> : 嘟囔  
> URL: https://newdivide2014.github.io/zh/posts/huawei-switch/  

