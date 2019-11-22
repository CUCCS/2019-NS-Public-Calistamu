# 网络监听
## 实验完成
- []ARP欺骗及监听者检测
- []ARP攻击
## 实验环境
![](images/network.jpg)
环境测试
![](images/networkok.png)
* 最初```arp -n```两个kali没有对方(忘了截图)，互相ping过以后，ip地址在双方的arp缓存表中出现。
* 互相ping的时候看到gateway-debian网关中有收到广播包，为了对比效果，attakcer-kali ping网关，看到网关收到了request,发送了reply。因此，在默认信任的内网中，发送的包能被网络中的所有主机收到，但只有目标主机会回应，在此原理上进行实验。
## 实验步骤

