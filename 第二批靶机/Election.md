
## 扫描

```
发现开放了22和80端口
```
## 服务枚举
```
对22端口进行尝试，发现可以使用密码登录
```

## web枚举
```
对网站根路径进行扫描。

/javascript           (Status: 301) [Size: 321] [--> http://192.168.80.141/javascript/]
/robots.txt           (Status: 200) [Size: 30]
/election             (Status: 301) [Size: 319] [--> http://192.168.80.141/election/]
/phpmyadmin           (Status: 301) [Size: 321] [--> http://192.168.80.141/phpmyadmin/]
Progress: 106001 / 1764488 (6.01%)

查看robots.txt后发现了几个可能的目录？
admin
wordpress
user
election
发现只有election可以访问。

对扫描出来的信息进行查看，发现了phpmyadmin的登录页，进行弱密码尝试后没有成功。

查看election页面，查看后发现有一个可以输入的地方，经过尝试应该时5位数字编号，用burp进行爆破没有爆破出有价值的信息。继续对/election目录进行扫描


/index.php            (Status: 200) [Size: 7003]
/media                (Status: 301) [Size: 325] [--> http://192.168.80.141/election/media/]
/themes               (Status: 301) [Size: 326] [--> http://192.168.80.141/election/themes/]
/data                 (Status: 301) [Size: 324] [--> http://192.168.80.141/election/data/]
/admin                (Status: 301) [Size: 325] [--> http://192.168.80.141/election/admin/]
/lib                  (Status: 301) [Size: 323] [--> http://192.168.80.141/election/lib/]
/languages            (Status: 301) [Size: 329] [--> http://192.168.80.141/election/languages/]
/js                   (Status: 301) [Size: 322] [--> http://192.168.80.141/election/js/]
/card.php             (Status: 200) [Size: 1935]

发现了card.php文件，对文件进行查看是一对01串，对数据进行解码。


用xxd与bc工具进行解码

for i in $(cat bin.txt);do echo "obase=16;ibase=2;$i"|bc >>result.txt;done

cat result.txt | paste -sd ''|xxd -r -p

发现解码完又是一串01，再进行一次重复解码


得到一个可能的口令？
user:1234733#2

对发现的phpmyadmin进行尝试，发现不成功。



查看/election目录扫描出来的结果

查看admin目录，又是一个需要输入id的验证框，用burp对验证框数字进行尝试，最终发现了1234这个数字是administrator账户的id，将上面得到的口令密码再次进行尝试，发现依旧没办法登录。

使用上面的到的凭据对ssh进行尝试，没有登录成功。

用收集到的所有数据，使用burpsuite对phpmyadmin目录进行爆破尝试，没有爆破出结果


对得到的所有目录进行OPTIONS发包尝试，也没有发现目录可以PUT


继续对admin目录进行爆破
/index.php            (Status: 200) [Size: 8964]
/img                  (Status: 301) [Size: 329] [--> http://192.168.80.141/election/admin/img/]
/plugins              (Status: 301) [Size: 333] [--> http://192.168.80.141/election/admin/plugins/]
/css                  (Status: 301) [Size: 329] [--> http://192.168.80.141/election/admin/css/]
/ajax                 (Status: 301) [Size: 330] [--> http://192.168.80.141/election/admin/ajax/]
/live.php             (Status: 200) [Size: 22]
/js                   (Status: 301) [Size: 328] [--> http://192.168.80.141/election/admin/js/]
/components           (Status: 301) [Size: 336] [--> http://192.168.80.141/election/admin/components/]
/logout.php           (Status: 200) [Size: 83]
/inc                  (Status: 301) [Size: 329] [--> http://192.168.80.141/election/admin/inc/]
/logs                 (Status: 301) [Size: 330] [--> http://192.168.80.141/election/admin/logs/]
/logs.php             (Status: 200) [Size: 22]
/dashboard.php        (Status: 200) [Size: 22]
/guru.php             (Status: 200) [Size: 22]



最终在http://192.168.80.141/election/admin/logs/system.log中又发现了一组凭据
[2020-01-01 00:00:00] Assigned Password for the user love: P@$$w0rd@123
[2020-04-03 00:13:53] Love added candidate 'Love'.
[2020-04-08 19:26:34] Love has been logged in from Unknown IP on Firefox (Linux).
[2024-01-12 19:52:09] Unknown IP is blocked from system. Cause: Brute-force @1234's password.
[2024-01-12 20:00:41]  has been logged out from Unknown IP.


用得到的凭据进行ssh登录，发现登录成功
```

## 提权

```
进行基本枚举后发现了suid权限中有一个/usr/local/Serv-U/Serv-U这个程序，进到相应目录进行查看，发现了 Serv-U-StartupLog.txt，查看后看到了Serv-U程序的版本为15.1

searchsploit Serv-U 15.1
发现了可以提权的利用程序。
kali中下载，然后搬运到靶机中执行脚本，发现提权成功
```
![[Pasted image 20240113103343.png]]