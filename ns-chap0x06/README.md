# 网络与系统渗透
[参考文献：从信息收集到入侵提权](https://blog.csdn.net/m0_37268841/article/details/79798561)
## 实验步骤
1. ping hack-test.com 获得网站服务器ip地址173.236.164.23
2. 使用[sameip.org](https://www.sameip.org/ip/)根据Ip地址查找同一台服务器上服务的所有站点，但是我这里出现了500错误。因为此次是尝试，抛开服务器上的其它网站，只针对目标网站来进行入侵检测。
![](images/500.png)
所以使用枚举DNSserver的主机名
```
nmap --script dns-brute hack-test.com
```
![](images/dnsserver.png)

3. 找网站的DNS记录  
a.[who.is](https://who.is/)找网站的DNS记录
![](images/whoisresult1.png)
![](images/whoisresult2.png)
b.终端输入```whois hack-test.com```获得网站域名的注册信息、电话、邮箱、地址、web服务器
![](images/whoisresult3.jpg)
4. 获取网站服务器操作系统类型和服务器版本
![](images/whatweb.png)
5. 用Nmap查看网站服务器开放的端口  
a.查看运行的服务```nmap -sV hack-test.com```![](images/runningserver.png)
b.查看操作系统版本```nmap -O hack-test.com```![](images/osversion.png)
6. Nikto是一个比较全面的网页扫描器，用Nikto收集漏洞信息```nikto -h hack-test.com```  
[nikto官方手册](https://cirt.net/nikto2-docs/)    
[nikto快速入门](https://blog.csdn.net/freeking101/article/details/72872502)  
![](images/nikto.png)
7. 用web应用扫描器  
[kali上安装w3af](https://blog.csdn.net/f786548139/article/details/80604586)  
* 打算物理机安装docker使用，虚拟机是用不了了，折腾了很久，终于虚拟机可以用了
![](images/nosql.png)
因此我只做到了这里，没有继续sql注入