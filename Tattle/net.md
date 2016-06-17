1. 
基础知识：什么是TCP/IP、UDP、Socket<br>
    TCP/IP(Transmission Control Protocol/Internet Protocol)<br>
    UDP(User Data Protocol)<br>
    网络模型图：
    ![](../1.jpg)
<br>那么Socket在那呢？
  ![](../12.jpg)
     <br>  Socket是应用层与TCP/IP协议族通信的中间软件抽象层，它是一组接口。在设计模式中，Socket其实就是一个门面模式，它把复杂的TCP/IP协议族隐藏在Socket接口后面，对用户来说，一组简单的接口就是全部，让Socket去组织数据，以符合指定的协议。<br>
      ![](../32.jpg)
 
1.  
HTTP的过程和原理

1. 
TCP 连接的过程和特点

1. 
TCP为什么需要三次握手？两次可以吗？

1. 
TCP四次挥手

1. 
拥塞控制

1. 
UDP与TCP的区别，应用场景

1. 
UDP与TCP优缺点

1. 
session放在哪里？如何保存绘画状态

1. 
访问www.163.com的过程，以及使用的协议

1. 
域名解析过程及协议

* 
ARP过程

1. 
ABC 类地址

* 
常用的端口号

| 层数 | 协议与端口号 | 备注 |
| -- | -- | -- |
| 1 物理层 |  | 负责比特信号的传播 |
| 2 数据链路层 |  | 帧 |
| 3 网络层 | IP、ARP、ICMP、RIP | 数据报 |
| 4 传输层 | TCP、UDP | 数据报，屏蔽底层细节 |
| 5 会话层 | |  |
| 6 表示层 | |  |
| 7 应用层 | DNS-53、FTP-20/21、TELNET、WWW、SMTP、POP3、DHCP |  |

* 
nignx的异步模型与事件管理


[返回目录](README.md)