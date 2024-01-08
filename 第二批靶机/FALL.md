## 扫描

可以枚举的服务有smb mysql ssh 
> 进行简单枚举发现没有暴露点

## web枚举

```
目录扫描结果
Target: http://192.168.80.137/

[13:12:17] Starting:
[13:12:19] 403 -  220B  - /.fishsrv.pl
[13:12:20] 403 -  220B  - /.ht_wsr.txt
[13:12:20] 403 -  223B  - /.htaccess.bak1
[13:12:20] 403 -  223B  - /.htaccess.orig
[13:12:20] 403 -  225B  - /.htaccess.sample
[13:12:20] 403 -  223B  - /.htaccess.save
[13:12:20] 403 -  224B  - /.htaccess_extra
[13:12:20] 403 -  221B  - /.htaccess_sc
[13:12:20] 403 -  221B  - /.htaccessOLD
[13:12:20] 403 -  213B  - /.htm
[13:12:20] 403 -  223B  - /.htaccess_orig
[13:12:20] 403 -  221B  - /.htaccessBAK
[13:12:20] 403 -  222B  - /.htaccessOLD2
[13:12:20] 403 -  223B  - /.htpasswd_test
[13:12:20] 403 -  219B  - /.htpasswds
[13:12:20] 403 -  220B  - /.httr-oauth
[13:12:20] 403 -  214B  - /.html
[13:12:24] 403 -  218B  - /.user.ini
[13:12:29] 403 -  221B  - /accounts.cgi
[13:12:29] 403 -  220B  - /accounts.pl
[13:12:30] 403 -  216B  - /adm.cgi
[13:12:30] 403 -  215B  - /adm.pl
[13:12:30] 301 -  236B  - /admin  ->  http://192.168.80.137/admin/
[13:12:31] 403 -  218B  - /admin.cgi
[13:12:32] 403 -  217B  - /admin.pl
[13:12:32] 302 -    0B  - /admin/  ->  http://192.168.80.137/admin/login.php
[13:12:33] 302 -    0B  - /admin/index.php  ->  http://192.168.80.137/admin/login.php
[13:12:33] 200 -    4KB - /admin/login.php
[13:12:43] 403 -  218B  - /apply.cgi
[13:12:44] 200 -    2KB - /assets/
[13:12:44] 301 -  237B  - /assets  ->  http://192.168.80.137/assets/
[13:12:44] 403 -  221B  - /AT-admin.cgi
[13:12:44] 403 -  217B  - /auth.cgi
[13:12:44] 403 -  216B  - /auth.pl
[13:12:45] 403 -  219B  - /awstats.pl
[13:12:48] 403 -  221B  - /cachemgr.cgi
[13:12:48] 403 -  217B  - /cgi-bin/
[13:12:49] 403 -  216B  - /cgi.pl/
[13:12:49] 403 -  220B  - /Cgishell.pl
[13:12:51] 404 -   16B  - /composer.phar
[13:12:51] 200 -    0B  - /config.php
[13:12:55] 403 -  220B  - /dcadmin.cgi
[13:12:55] 403 -  218B  - /debug.cgi
[13:12:56] 301 -  234B  - /doc  ->  http://192.168.80.137/doc/
[13:12:56] 200 -   24B  - /doc/
[13:12:58] 200 -   80B  - /error.html
[13:12:59] 200 -    1KB - /favicon.ico
[13:13:01] 403 -  218B  - /gbpass.pl
[13:13:03] 403 -  223B  - /hndUnblock.cgi
[13:13:06] 404 -  231B  - /index.php/login/
[13:13:09] 301 -  234B  - /lib  ->  http://192.168.80.137/lib/
[13:13:09] 200 -   24B  - /lib/
[13:13:11] 403 -  218B  - /login.cgi
[13:13:11] 403 -  217B  - /login.pl
[13:13:11] 403 -  216B  - /logs.pl
[13:13:14] 403 -  220B  - /members.cgi
[13:13:14] 403 -  219B  - /members.pl
[13:13:15] 301 -  238B  - /modules  ->  http://192.168.80.137/modules/
[13:13:15] 200 -    3KB - /modules/
[13:13:16] 403 -  221B  - /mt-check.cgi
[13:13:16] 403 -  215B  - /mt.cgi
[13:13:16] 403 -  222B  - /mt-xmlrpc.cgi
[13:13:19] 403 -  216B  - /out.cgi
[13:13:20] 403 -  220B  - /perlcmd.cgi
[13:13:20] 403 -  230B  - /perl-reverse-shell.pl
[13:13:20] 404 -   16B  - /php-cs-fixer.phar
[13:13:21] 200 -   17B  - /phpinfo.php
[13:13:23] 404 -   16B  - /phpunit.phar
[13:13:26] 403 -  221B  - /ps_admin.cgi
[13:13:30] 200 -   79B  - /robots.txt
[13:13:34] 403 -  219B  - /signin.cgi
[13:13:34] 403 -  218B  - /signin.pl
[13:13:41] 200 -   80B  - /test.php
[13:13:41] 403 -  217B  - /test.cgi
[13:13:42] 200 -    1KB - /tmp/
[13:13:42] 301 -  234B  - /tmp  ->  http://192.168.80.137/tmp/
[13:13:42] 403 -  219B  - /tmp/cgi.pl
[13:13:42] 403 -  224B  - /tmp/Cgishell.pl
[13:13:42] 403 -  223B  - /tmp/domaine.pl
[13:13:44] 301 -  238B  - /uploads  ->  http://192.168.80.137/uploads/
[13:13:44] 200 -    0B  - /uploads/
[13:13:50] 403 -  221B  - /WebShell.cgi

Task Completed


```
## web后台枚举
>对页面信息进行收集后发现了个用户patrick，经过目录扫描发现了admin这个目录，通过忘记密码功能对admin和root还有qiu进行了测试，发现了patrick可以让页面发生跳转。最终确定了cms的后台用户有patrick，对后台进行爆破，最终未发现可以登录的凭据


> 访问后发现提示需要以get方式传递参数
![[Pasted image 20240108154247.png]]

> 进行fuzz测试

`wfuzz -c -w /usr/share/wordlists/dirb/commit.txt http://192.168.80.137/test.php?FUZZ=index.php`

> 最终经过测试发现了file这个参数，通过包含/etc/passwd发现了有/bin/bash环境的用户。qiu和root

#### 用得到的包含路径进行服务器信息枚举
```
/etc/passwd
/home/.ssh/id_rsa
/home/.ssh/authorized_keys
得到qiu的私钥
进行ssh登录，发现登录成功
```


## 提权

```
查看家目录的历史命令文件，发现了一个疑似凭据的字符串
sudo /bin/bash 提权

```
![[Pasted image 20240108155714.png]]










