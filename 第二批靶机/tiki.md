## 扫描
![[Pasted image 20231230162113.png]]
>**先对smb进行查看**
![[Pasted image 20231230162246.png]]

> **得到Silky的cms凭据

## web渗透

> **首先查看robots.txt文件发现了/tiki/目录。用smb得到的凭据登录发现了一段文字，说有个cve漏洞，还有管理账号名为admin。**

![[Pasted image 20231230162912.png]]

> **网上搜索这个cms的漏洞发现了可以爆破指定次数然后空白密码进行管理员登陆**

![[Pasted image 20231230163108.png]]
>**用burpsuite抓包发现，登录页面有token认证**
![[Pasted image 20231230163434.png]]

![[Pasted image 20231230163529.png]]
![[Pasted image 20231230163628.png]]

> **payload2 随便找个字典
![[Pasted image 20231230164712.png]]

> **线程设为1

![[Pasted image 20231230163904.png]]

> **当爆破进入到达100多左右，burpsuite进行放包，发现已经登陆admin

![[Pasted image 20231230165226.png]]

> **最终在admin的list pages中发现了Credentials这个页
![[Pasted image 20231230165328.png]]
> 又得到一组凭据，
![[Pasted image 20231230162738.png]]

>**尝试ssh登录后，发现登录成功，并且sudo为ALL，直接进行提权

![[Pasted image 20231230165656.png]]
> flag

![[Pasted image 20231230165757.png]]