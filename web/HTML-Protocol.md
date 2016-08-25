#HTTP-Protocol
* 
电脑上访问一个网页，整个过程是怎么样的：DNS、HTTP、TCP、OSPF、IP、ARP。

HTTP协议（HyperText TransferProtocol，超文本传输协议）是用于从WWW服务器传输超文本到本地浏览器的传送协议。是一个无状态的协议，处于应用层。

![](TCPIP.jpg)

HTTP只能由客户端发起请求，然后服务器端相应

![](5657919_2.jpg)

### 工作流程：


1. 
建立连接
1. 
客户机发送请求    格式如下：Method Request-URI HTTP-Version CRLF  
1. 
服务器得到请求，发送相应的响应信息           HTTP-Version Status-Code Reason-Phrase CRLF
1. 
客户机解析并显示

注：
1. 
请求方法：<br
GET     请求获取Request-URI所标识的资源<br>
POST    在Request-URI所标识的资源后附加新的数据<br>
HEAD    请求获取由Request-URI所标识的资源的响应消息报头<br>
PUT     请求服务器存储一个资源，并用Request-URI作为其标识<br>
DELETE  请求服务器删除Request-URI所标识的资源<br>
TRACE   请求服务器回送收到的请求信息，主要用于测试或诊断<br>
CONNECT 保留将来使用<br>
OPTIONS 请求查询服务器的性能，或者查询与资源相关的选项和需求
1. 
响应状态：<br>
1xx：指示信息--表示请求已接收，继续处理<br>
2xx：成功--表示请求已被成功接收、理解、接受<br>
3xx：重定向--要完成请求必须进行更进一步的操作<br>
4xx：客户端错误--请求有语法错误或请求无法实现<br>
5xx：服务器端错误--服务器未能实现合法的请求<br>
常见状态代码、状态描述、说明：<br>
200 OK      //客户端请求成功<br>
400 Bad Request  //客户端请求有语法错误，不能被服务器所理解<br>
401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 <br>
403 Forbidden  //服务器收到请求，但是拒绝提供服务<br>
404 Not Found  //请求资源不存在，eg：输入了错误的URL<br>
500 Internal Server Error //服务器发生不可预期的错误<br>
503 Server Unavailable  //服务器当前不能处理客户端的请求，一段时间后可能恢复正常<br>



---



### 消息：
请求消息和响应消息都是由开始行（对于请求消息，开始行就是请求行，对于响应消息，开始行就是状态行），消息报头（可选），空行（只有CRLF的行），消息正文（可选）组成<br>HTTP消息报头包括**普通报头、请求报头、响应报头、实体报头。**
每一个报头域都是由**名字+“：”+空格+值 **组成，消息报头域的名字是大小写无关的。<br>
[参考](http://www.cnblogs.com/li0803/archive/2008/11/03/1324746.html)

##Request
Request对象的作用是与客户端交互，收集客户端的Form、Cookies、超链接，或者收集服务器端的环境变量。

[返回目录](README.md)