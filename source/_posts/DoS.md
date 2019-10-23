---        
#     <center>DOS攻击</center>
DoS(Denial of Service)是对服务器的一种攻击手段，通过耗尽服务器的网络或系统资源，达到服务器无法给正常用户提供服务的目的。一台计算机的攻击力有限，对于大型服务器，一般是利用大量计算机攻击统一目标，这种称为DDoS(Distributed Denial of Service)

##     SYN-FLOOD攻击
SYN攻击是针对TCP协议的三次握手进行的一种DoS攻击

第一次握手：建立连接时，客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认；

第二次握手：服务器收到syn包，必须确认客户的syn（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；

第三次握手：客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。

服务器有一个队列记录尚未确认连接客户端的信息，完成第二次握手后，服务器就会将对应的客户端加入该队列，直到完成三次握手或超过一定时间才会将客户端从该队列删除。

SYN攻击就是伪造大量客户端对服务器发起连接请求，占满服务器端的半连接队列资源，使服务器无法响应正常客户的请求。

##       HPING 3 进行SYN攻击
攻击机: kali  172.16.111.128

靶机: metasploitable 3   172.16.111.131

使用nmap简单扫描靶机信息

![](https://i.loli.net/2019/10/23/7SusvzjLMyxRUTQ.png)
使用hping3 进行SYN--flood

```
hping3 172.16.111.131 -S -p 80 --flood --rand-source  
-S 添加SYN头部 -p 指定端口 --flood 洪水模式，尽量快的发包 --rand-source 伪造随机源
```

![](https://i.loli.net/2019/10/23/VUw1D723NkFIlrJ.png)

可以看出靶机受到攻击后CPU占用显著提高，对靶机系统资源影响还是比较严重的。


 2019-10-14 21:48:02

---        
