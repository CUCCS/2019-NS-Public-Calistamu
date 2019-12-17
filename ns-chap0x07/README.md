# Web 应用漏洞攻防
## 实验目的
* 了解常见 Web 漏洞训练平台；
* 了解 常见 Web 漏洞的基本原理；
* 掌握 OWASP Top 10 及常见 Web 高危漏洞的漏洞检测、漏洞利用和漏洞修复方法；
## 实验要求
- []WebGoat 7.1
- []WebGoat 8.0
- []DVWA
- []juicy shop
- []Vulhub
* 每个实验环境完成不少于 5 种不同漏洞类型的漏洞利用练习；
* 可选）使用不同于官方教程中的漏洞利用方法完成目标漏洞利用练习；
* （可选）最大化 漏洞利用效果实验；
* （可选）定位缺陷代码；
* （可选）尝试从源代码层面修复漏洞；
## 实验参考
[Web安全攻防靶场之WebGoat](http://www.xianxianlabs.com/2018/06/03/webgoat1/#i)  
[这一系列文章用于学原理](https://blog.csdn.net/ggf123456789/article/details/23562103)  
[OWASP Top10 2017](http://www.owasp.org.cn/owasp-project/OWASPTop102017v1.3.pdf)
## 实验环境
1. 下载老师给的实验环境文件
```
git clone https://github.com/c4pr1c3/ctf-games.git
```
2. 安装docker,webgoat,juicy shop，dvwa
```
#开启docker服务
sudo service docker start
#后台启动并运行容器
docker-compose up -d
```
* docker、dockerfile、docker-compose区别：  
docker:容器，隔离作用  
dockerfile:用来构建镜像的文本文件,包含构建镜像所需的指令和说明，因为并不是直接生成容器，是构建了镜像，再运行镜像运行容器。   
docker-compose:定义和运行多容器 Docker 应用程序的工具。通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务。  
[docker教程](https://www.runoob.com/docker/docker-tutorial.html)

配置如图
![](images/platform.png)
3. 准备配置代理，会BurpSuite的基础使用，在训练过程中熟悉使用  
[BurpSuite实战指南](https://t0data.gitbooks.io/burpsuite/content/chapter2.html)  
4. [关于同时运行docker和burp suite虚拟机卡死的解决](https://www.jianshu.com/p/77435e67980c)
## 实验步骤
### WebGoat7.0.1漏洞利用
[webgoat7.1实战指南](https://www.cnblogs.com/wuweidong/p/8677431.html)
#### 一、Http Basics
目标：HTTP 请求的基本操作原理  
输入'webgoat'点击'Go'。burpsuite的结果，和用火狐浏览器'网络'中看到的结果，提交的用户名是'webgoat'，method是POST。
![](images/httpbasic.png)
#### 二、Access Control Flaws
##### 1.Using an Access Control Matrix
目标：了解访问权限规则
* 第一种方法：依次试（红色字体提示当前用户是否有权限），反正这次作业也不多。
* 第二种方法：使用intruder修改请求参数，来获取不同的请求应答，从而遍历破解。
第二种方法步骤：  
1. 先择可能存在问题的日志，此次选一个method为'POST'的日志，右键'send to intruder'
2. 如下设置
![](images/intruder1.jpg)
![](images/intruder2.png)
![](images/intruder3.jpg)
3. 攻击结果
![](images/intruder4.png)
得到权限矩阵如下
![](images/intruder5.jpg)
##### 2.Bypass a Path Based Access Control Scheme
目标：攻击者可以使用相对路径访问那些通常任何人都不能直接访问或直接请求就会被拒绝的文件  
1. 当前路径：
![](images/bypass1.png)
访问其中某一个资源，发现在同一个文件夹下
![](images/bypass2.png)
2. 通过修改raw里面的路径来进行路径切换，从而访问我们想要访问的资源。根据'POST'请求，找到我们的目标日志，然后'send to repeater',更改'File'的值.

* 不可以直接更改也是搞了很久

![](images/bypass3.png)
* 之前一直以为是重定位到我刚刚选的CSRF.html,也是没有认真读题，目标是'WEB-INF/spring-security.xml',而他的实际路径应该是'./extract/webapps/WebGoat/WEB-INF/spring-security.xml',因此有了上图的相对路径
* 'Go'以后发现绿色的小勾勾没有点亮，很奇怪.右键'Request in browser'--'in current browser session'得到的url，copy下来在浏览器中新标签页访问后，刷新webgoat页面，亮了。
##### 3.LAB: Role Based Access Control
###### 3.1 Stage 1: Bypass Business Layer Access Control
目标：让普通用户Tom能够完成删除个人资料的功能
1. 找出可以进行删除功能的用户。  
找到POST包send to intruder。  
再进行如下设置
![](images/bypass3.1-1.png)
* 因为一共有12个用户
![](images/bypass3.1-2.png)
![](images/bypass3.1-3.png)
![](images/bypass3.1-4.png)
在结果中看到可以删除的用户在'action'中多了'deleteprofile'。因此，burpsuite更改action的值后访问新页面即可
###### 3.2 Stage 2: Add Business Layer Access Control.
###### 3.3 Stage 3: Breaking Data LayerAccess Control
###### 3.4 Stage 4: Add Data Layer Access Control.

