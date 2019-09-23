# 无线路由器/无线接入点（AP）配置

## 实验完成情况

- []设置AP的管理员用户名和密码  
- []设置SSID广播和非广播模式  
- []配置不同的加密方式  
- []设置AP管理密码  
- []配置无线路由器使用自定义的DNS解析服务器   
- []配置DHCP和禁用DHCP  
- []开启路由器/AP的日志记录功能（对指定事件记录）  
- []配置AP隔离(WLAN划分)功能    
- []设置MAC地址过滤规则（ACL地址过滤器）  
- []查看WPS功能的支持情况  
- []查看AP/无线路由器支持哪些工作模式  

## 实验步骤

1.安装openwrt  
[openwrt安装到virtualbox指南](https://openwrt.org/start?id=zh/docs/guide-user/virtualization/virtualbox-vm?_blank)
2.Host-only网络设置
![](sethostonly.png)
3.网卡设置  
&#8195;网卡一：NAT&#8195;网卡二：Host-only&#8195;网卡三：桥接  
4.

