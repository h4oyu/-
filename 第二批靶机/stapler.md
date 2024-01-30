

# 扫描

```bash

PORT      STATE  SERVICE     VERSION
20/tcp    closed ftp-data
21/tcp    open   ftp         vsftpd 2.0.8 or later
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to 192.168.80.1
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 550 Permission denied.
22/tcp    open   ssh         OpenSSH 7.2p2 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 81:21:ce:a1:1a:05:b1:69:4f:4d:ed:80:28:e8:99:05 (RSA)
|   256 5b:a5:bb:67:91:1a:51:c2:d3:21:da:c0:ca:f0:db:9e (ECDSA)
|_  256 6d:01:b7:73:ac:b0:93:6f:fa:b9:89:e6:ae:3c:ab:d3 (ED25519)
53/tcp    open   domain      dnsmasq 2.75
| dns-nsid:
|_  bind.version: dnsmasq-2.75
80/tcp    open   http        PHP cli server 5.5 or later
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
123/tcp   closed ntp
137/tcp   closed netbios-ns
138/tcp   closed netbios-dgm
139/tcp   open   netbios-ssn Samba smbd 4.3.9-Ubuntu (workgroup: WORKGROUP)
666/tcp   open   doom?
| fingerprint-strings:
|   NULL:
|     message2.jpgUT
|     QWux
|     "DL[E
|     #;3[
|     \xf6
|     u([r
|     qYQq
|     Y_?n2
|     3&M~{
|     9-a)T
|     L}AJ
|_    .npy.9
3306/tcp  open   mysql       MySQL 5.7.12-0ubuntu1
| mysql-info:
|   Protocol: 10
|   Version: 5.7.12-0ubuntu1
|   Thread ID: 7
|   Capabilities flags: 63487
|   Some Capabilities: ODBCClient, Support41Auth, Speaks41ProtocolOld, IgnoreSpaceBeforeParenthesis, ConnectWithDatabase, DontAllowDatabaseTableColumn, SupportsTransactions, IgnoreSigpipes, LongColumnFlag, SupportsLoadDataLocal, InteractiveClient, FoundRows, SupportsCompression, Speaks41ProtocolNew, LongPassword, SupportsAuthPlugins, SupportsMultipleResults, SupportsMultipleStatments
|   Status: Autocommit
|   Salt: \\x01hy\x15x{\x1A')LWVh kH\x18'>
|_  Auth Plugin Name: mysql_native_password
12380/tcp open   http        Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port666-TCP:V=7.94SVN%I=7%D=1/21%Time=65AC9491%P=x86_64-pc-linux-gnu%r(
SF:NULL,2D58,"PK\x03\x04\x14\0\x02\0\x08\0d\x80\xc3Hp\xdf\x15\x81\xaa,\0\0
SF:\x152\0\0\x0c\0\x1c\0message2\.jpgUT\t\0\x03\+\x9cQWJ\x9cQWux\x0b\0\x01
SF:\x04\xf5\x01\0\0\x04\x14\0\0\0\xadz\x0bT\x13\xe7\xbe\xefP\x94\x88\x88A@
SF:\xa2\x20\x19\xabUT\xc4T\x11\xa9\x102>\x8a\xd4RDK\x15\x85Jj\xa9\"DL\[E\x
SF:a2\x0c\x19\x140<\xc4\xb4\xb5\xca\xaen\x89\x8a\x8aV\x11\x91W\xc5H\x20\x0
SF:f\xb2\xf7\xb6\x88\n\x82@%\x99d\xb7\xc8#;3\[\r_\xcddr\x87\xbd\xcf9\xf7\x
SF:aeu\xeeY\xeb\xdc\xb3oX\xacY\xf92\xf3e\xfe\xdf\xff\xff\xff=2\x9f\xf3\x99
SF:\xd3\x08y}\xb8a\xe3\x06\xc8\xc5\x05\x82>`\xfe\x20\xa7\x05:\xb4y\xaf\xf8
SF:\xa0\xf8\xc0\^\xf1\x97sC\x97\xbd\x0b\xbd\xb7nc\xdc\xa4I\xd0\xc4\+j\xce\
SF:[\x87\xa0\xe5\x1b\xf7\xcc=,\xce\x9a\xbb\xeb\xeb\xdds\xbf\xde\xbd\xeb\x8
SF:b\xf4\xfdis\x0f\xeeM\?\xb0\xf4\x1f\xa3\xcceY\xfb\xbe\x98\x9b\xb6\xfb\xe
SF:0\xdc\]sS\xc5bQ\xfa\xee\xb7\xe7\xbc\x05AoA\x93\xfe9\xd3\x82\x7f\xcc\xe4
SF:\xd5\x1dx\xa2O\x0e\xdd\x994\x9c\xe7\xfe\x871\xb0N\xea\x1c\x80\xd63w\xf1
SF:\xaf\xbd&&q\xf9\x97'i\x85fL\x81\xe2\\\xf6\xb9\xba\xcc\x80\xde\x9a\xe1\x
SF:e2:\xc3\xc5\xa9\x85`\x08r\x99\xfc\xcf\x13\xa0\x7f{\xb9\xbc\xe5:i\xb2\x1
SF:bk\x8a\xfbT\x0f\xe6\x84\x06/\xe8-\x17W\xd7\xb7&\xb9N\x9e<\xb1\\\.\xb9\x
SF:cc\xe7\xd0\xa4\x19\x93\xbd\xdf\^\xbe\xd6\xcdg\xcb\.\xd6\xbc\xaf\|W\x1c\
SF:xfd\xf6\xe2\x94\xf9\xebj\xdbf~\xfc\x98x'\xf4\xf3\xaf\x8f\xb9O\xf5\xe3\x
SF:cc\x9a\xed\xbf`a\xd0\xa2\xc5KV\x86\xad\n\x7fou\xc4\xfa\xf7\xa37\xc4\|\x
SF:b0\xf1\xc3\x84O\xb6nK\xdc\xbe#\)\xf5\x8b\xdd{\xd2\xf6\xa6g\x1c8\x98u\(\
SF:[r\xf8H~A\xe1qYQq\xc9w\xa7\xbe\?}\xa6\xfc\x0f\?\x9c\xbdTy\xf9\xca\xd5\x
SF:aak\xd7\x7f\xbcSW\xdf\xd0\xd8\xf4\xd3\xddf\xb5F\xabk\xd7\xff\xe9\xcf\x7
SF:fy\xd2\xd5\xfd\xb4\xa7\xf7Y_\?n2\xff\xf5\xd7\xdf\x86\^\x0c\x8f\x90\x7f\
SF:x7f\xf9\xea\xb5m\x1c\xfc\xfef\"\.\x17\xc8\xf5\?B\xff\xbf\xc6\xc5,\x82\x
SF:cb\[\x93&\xb9NbM\xc4\xe5\xf2V\xf6\xc4\t3&M~{\xb9\x9b\xf7\xda-\xac\]_\xf
SF:9\xcc\[qt\x8a\xef\xbao/\xd6\xb6\xb9\xcf\x0f\xfd\x98\x98\xf9\xf9\xd7\x8f
SF:\xa7\xfa\xbd\xb3\x12_@N\x84\xf6\x8f\xc8\xfe{\x81\x1d\xfb\x1fE\xf6\x1f\x
SF:81\xfd\xef\xb8\xfa\xa1i\xae\.L\xf2\\g@\x08D\xbb\xbfp\xb5\xd4\xf4Ym\x0bI
SF:\x96\x1e\xcb\x879-a\)T\x02\xc8\$\x14k\x08\xae\xfcZ\x90\xe6E\xcb<C\xcap\
SF:x8f\xd0\x8f\x9fu\x01\x8dvT\xf0'\x9b\xe4ST%\x9f5\x95\xab\rSWb\xecN\xfb&\
SF:xf4\xed\xe3v\x13O\xb73A#\xf0,\xd5\xc2\^\xe8\xfc\xc0\xa7\xaf\xab4\xcfC\x
SF:cd\x88\x8e}\xac\x15\xf6~\xc4R\x8e`wT\x96\xa8KT\x1cam\xdb\x99f\xfb\n\xbc
SF:\xbcL}AJ\xe5H\x912\x88\(O\0k\xc9\xa9\x1a\x93\xb8\x84\x8fdN\xbf\x17\xf5\
SF:xf0\.npy\.9\x04\xcf\x14\x1d\x89Rr9\xe4\xd2\xae\x91#\xfbOg\xed\xf6\x15\x
SF:04\xf6~\xf1\]V\xdcBGu\xeb\xaa=\x8e\xef\xa4HU\x1e\x8f\x9f\x9bI\xf4\xb6GT
SF:Q\xf3\xe9\xe5\x8e\x0b\x14L\xb2\xda\x92\x12\xf3\x95\xa2\x1c\xb3\x13\*P\x
SF:11\?\xfb\xf3\xda\xcaDfv\x89`\xa9\xe4k\xc4S\x0e\xd6P0");
Aggressive OS guesses: Linux 3.2 - 4.9 (95%), Linux 3.10 - 4.11 (92%), Linux 3.13 (92%), Linux 3.13 - 3.16 (92%), OpenWrt Chaos Calmer 15.05 (Linux 3.18) or Designated Driver (Linux 4.1 or 4.4) (92%), Linux 4.10 (92%), Android 5.0 - 6.0.1 (Linux 3.4) (92%), Linux 3.10 (92%), Linux 3.2 - 3.10 (92%), Linux 3.2 - 3.16 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: RED; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb2-time:
|   date: 2024-01-21T03:50:58
|_  start_date: N/A
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.3.9-Ubuntu)
|   Computer name: red
|   NetBIOS computer name: RED\x00
|   Domain name: \x00
|   FQDN: red
|_  System time: 2024-01-21T03:50:58+00:00
|_nbstat: NetBIOS name: RED, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled but not required

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   0.84 ms DESKTOP-SH1BMBR (172.26.32.1)
2   3.75 ms 192.168.80.150

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Jan 21 11:51:31 2024 -- 1 IP address (1 host up) scanned in 51.24 seconds
```
## **服务枚举**

**搜索公开的已知漏洞发现**
	vsftpd 2.0.8                      无
	Samba smbd 4.3.9           is_known_pipename
	OpenSSH 7.2p2                用户名枚举


**Samba和openssh**
```
发现samba有个漏洞 exploit/linux/samba/is_known_pipename，经过尝试可以直接得到shell并提权到root
```

>**枚举**

```bash
enum4linux -a 192.168.80.150
发现了很多用户，把发现的用户裁剪存成字典，用openssh的漏洞尝试有哪些可以登录成功
```
![[Pasted image 20240122162332.png]]
> **还发现了两个目录**
```

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        kathy           Disk      Fred, What are we doing here?
        tmp             Disk      All temporary files should be stored here
        IPC$            IPC       IPC Service (red server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            RED
```
> **连接并转储其中文件**

```
发现了几个文件和一个网站的备份wordpress，查看后并没有什么可以利用的
```

> **ftp支持匿名登录，登录后没有任何发现，用hydra爆破ssh端口，然后去查看web页**





## **web枚举**
> web共有三个可能的端口，80 ，12380 ，666


80端口有一个任意文件下载
http://192.168.80.150/.bashrc 可以直接下载到某个用户的.bashrc文件，尝试下载私钥/.ssh/id_rsa和authorized_keys后并没成功，目录爆破也没有任何发现，将http协议改为https协议，也没有任何变化

12380端口爆破也没爆破出任何信息，将http协议改为https后发现页面发生变化。检查robots.txt后发现了网站敏感目录
	
	User-agent: *
	Disallow: /admin112233/
	Disallow: /blogblog/

admin112233是个弹窗，没什么发现

blogblog是一个标准的wordpress页面，直接进行wpscan进行扫描

```
sudo wpscan --url https://192.168.80.150:12380/blogblog/ -e u --disable-tls-checks
sudo wpscan --url https://192.168.80.150:12380/blogblog/ -e vp --disable-tls-checks
sudo wpscan --url https://192.168.80.150:12380/blogblog/ -e vt --disable-tls-checks


对结果裁剪转储为字典
John
peter
john
elly
barry
heather
garry
harry
scott
kathy
tim
进行爆破
[SUCCESS] - garry / football
[SUCCESS] - harry / monkey
[SUCCESS] - scott / cookie
[SUCCESS] - kathy / coolgirl

对插件扫描的漏洞进行尝试，没有可以利用的，而且爆破速度很慢，再对/blogblog进行目录扫描
```
![[Pasted image 20240122182458.png]]

> 对wp-content/uploads/目录进行查看发现了一个视频播放插件advanced video？
> advanced-video-embed-embed-videos-or-playlists

>**从漏洞库查找**
![[Pasted image 20240122183022.png]]
> 改写exp 加入忽略证书验证
![[Pasted image 20240122184549.png]]
> **报错。搜索后继续改写**
![[Pasted image 20240122184655.png]]
>**执行成功**
![[Pasted image 20240122184820.png]]


**wget 下载upload中生成的图片**

```bash
wget https://192.168.80.150:12380/blogblog//wp-content/uploads/1095590242.jpeg --no-check-certificate
```

> **cat查看发现没有得到任何信息，利用失败**
![[Pasted image 20240122190328.png]]

> **查看wpscan结果发现，又出现了几个后台用户**
	
	[SUCCESS] - barry / washere
	[SUCCESS] - John / incorrect
	[SUCCESS] - john / incorrect
	[SUCCESS] - tim / thumb

> **继续对后台进行尝试，成功找到管理员john.尝试寻找错误页面写反弹shell，发现当前管理员无法修改页面内容，只能放弃。最后找到themes 点击add new themes 再点击upload themes，上传一个php的反弹shell，最后回到https://192.168.80.150:12380/blogblog/wp-content/uploads/去触发反弹shell**



[SUCCESS] - garry / football
[SUCCESS] - harry / monkey
[SUCCESS] - scott / cookie
[SUCCESS] - kathy / coolgirl
[SUCCESS] - barry / washere
[SUCCESS] - John / incorrect
[SUCCESS] - john / incorrect
[SUCCESS] - tim / thumb


## 提权

find / -perm -u=s -type f 2>/dev/null
/usr/bin/newuidmap
/usr/bin/chsh
/usr/bin/sudo
/usr/bin/chfn
/usr/bin/pkexec
/usr/bin/newgidmap
/usr/bin/at
/usr/bin/passwd
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/ubuntu-core-launcher
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/i386-linux-gnu/lxc/lxc-user-nic
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/authbind/helper
/bin/mount
/bin/umount
/bin/ping
/bin/fusermount
/bin/ping6
/bin/su

翻找家目录的.bash_history找到了peter的密码，登录后发现时ALL，直接sudo /bin/bash提权