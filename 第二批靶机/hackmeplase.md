

## web信息收集

```
发现main.js文件查看后发现隐藏目录/seeddms51x/seeddms-5.1.22/ 的后台登录页面

目录爆破发现了/seeddms51x/conf/settings.xml文档，文档中提供了mysql的账户密码
	seeddms：seeddms

```
## mysql

```
查看users表获取一组凭据
saket：Saket@#$1337

经过尝试，发现并不是web后台的账号密码
查看tblUsers表发现admin密码，经过尝试发现解不开

更改管理员账号的密码

update tblUsers set pwd="e10adc3949ba59abbe56e057f20f883e" where id=1;

成功登录后台

```


## 上传拿webshell

```
网上搜集这套dms的信息，发现了上传的路径为/seeddms51x/data/1048576/id/文件名，进行上传后得到shell

得到shell后使用saket用户的凭据，成功切换到saket。发现sudo为ALL，直接进行提权。sudo /bin/bash




```










