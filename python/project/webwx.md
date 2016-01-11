＃webwx登录模拟

[转载 http://www.tanhao.me/talk/1466.html/](http://www.tanhao.me/talk/1466.html/)

下面就详细解说一下微信Web版的流程：

1.微信服务器返回一个会话ID
微信Web版本不使用用户名和密码登录，而是采用二维码登录，所以服务器需要首先分配一个唯一的会话ID，用来标识当前的一次登录，通过请求地址：

https://login.weixin.qq.com/jslogin?appid=wx782c26e4c19acffb&redirect_uri=https%3A%2F%2Fwx.qq.com%2Fcgi-bin%2Fmmwebwx-bin%2Fwebwxnewloginpage&fun=new&lang=zh_CN&_=1377482012272（其中1377482012272这个值是当前距离林威治标准时间的毫秒）

服务器会返回如下的字符串：
window.QRLogin.code = 200; window.QRLogin.uuid = “DeA6idundY9VKn”;

而这个DeA6idundY9VKn（每一次都不同）字符串就是微信服务器返回给我们这次会话的ID。

2.通过会话ID获得二维码

既然微信Web版本是通过二维码进行登录，如何获得这个随机的二维码呢？答案就是利用刚才获得的ID去请求服务器生成的二维码，通过上面的ID我们组合得到以下的URL地址：

https://login.weixin.qq.com/qrcode/DeA6idundY9VKn?t=webwx

该请求返回的便是我们需要的二维码，此时需要用户在微信的手机版本中扫描这个二维码（我就搞不明白微信官方是如何想的，登录Web版本竟然还需要手机微信去配合登录，难道没有考虑我被迫选择Web微信就是因为手机不在身边这样的情形么？）

3.**轮询**手机端是否已经扫描二维码并确认在Web端登录

当获得二维码之后，就需要用户去手机端去扫描二维码，并获得用户的授权，此时我们并不知道用户何时完成这个操作，所以我们只有轮询，而轮询的地址就是：

https://login.weixin.qq.com/cgi-bin/mmwebwx-bin/login?uuid=DeA6idundY9VKn&tip=1&_=1377482045264（注意UUID和最后时间这两个参数）

如果服务器返回：

window.code=201;

则说明此时用户在手机端已经完成扫描，但还没有点击确认；

如果服务器返回：

window.redirect_uri=一个URL地址

则说明此时用户已经在手机端完成了授权过程，保存下这个URL地址下一步骤中使用。

4.访问登录地址，获得uin和sid

通过访问上一步骤中获得的URL地址，可以在服务器返回的Cookies中获得到wxuin和wxsid这两个值，这两值在后续的通信过程中都要使用到这两个值，并且Cookies中也需要包括这两项。

5.初使化微信信息

前面的步骤算是完成了这个复杂的登录过程，如果我们需要使用微信就需要获得当前用户的信息、好友列表等，还有一个关键的就是同步信息（后续与服务器轮询中需要使用同步信息），通过访问以下的链接：

https://wx.qq.com/cgi-bin/mmwebwx-bin/webwxinit?r=1377482058764（r依然是时间）

访问该链接需要使用POST，并且在Body中带上以下的JSON信息：