---          
#    <center>MITM攻击</center>
MITM(man in the middle)： 攻击方分别与通信两端A，B建立连接，攻击方伪装成B与A通信，伪装成A与B通信。A，B双方以为通信是安全可靠的，实际上攻击方成了双方通信的中转站，以达到对通信内容进行窃取，篡改的目的

##    ARP欺骗
当局域网中的计算机要访问外部网络时，要先广播发送ARP的包查询路由(网关)的MAC地址，此时如果攻击方伪装自己是网关，发送ARP应答包给目标机器，可以污染对方的ARP缓存表。使得目标计算机将数据包发给攻击方。

###    测试一
arp攻击靶机，攻击方伪装成网关

靶机: metasploitable 3 win2k8 

攻击方: kali 

攻击前，靶机信息如图，ip: 172.16.111.131  网关ip: 172.16.111.2

![](https://i.loli.net/2019/10/24/ayTkBFUpSnjiA62.png)

采用metasploit 的arp poisoning模块进行攻击

![](https://i.loli.net/2019/10/24/CvRmZtWHNk3hUsc.png)

攻击后，靶机浏览器无法正常浏览网页，查看arp信息如下，网关的MAC地址和攻击方地址一样。

![](https://i.loli.net/2019/10/24/MWeDhGrH9wfpKxa.png)

###    测试二
在上面的基础上，欺骗网关自己为靶机，并将他们发来的数据包转发出去。

再开启一个模块：
![](https://i.loli.net/2019/10/24/8IyVNaSpTmuUQgH.png)

然后终端输入：
```
echo 1 > /proc/sys/net/ipv4/ip_forward

默认值是0,改为1后开启ip转发功能
```
完成后，靶机又可以正常浏览网页。

使用Wireshark抓包

![](https://i.loli.net/2019/10/24/hYqaeMUjSoZrET1.png)

可以抓取到靶机与外网的流量包。

 2019-10-16 21:17:02

---         
