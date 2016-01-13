除了[基础模块1](func&moduler.md)和[基础模块2](http://www.jb51.net/article/57656.htm),还有[扩展模块](http://blog.csdn.net/lcyangcss/article/details/7249961)<br>

### 使用豆瓣或者其它源：


虽然用easy_install和pip来安装第三方库很方便,它们的原理其实就是从Python的官方源http://pypi.python.org/pypi 下载到本地，然后解包安装。不过因为某些原因，访问官方的pypi不稳定，很慢甚至有些还时不时的访问不了。 
在国内的强烈推荐豆瓣的源：
http://pypi.douban.com/simple/ 
注意后面要有/simple目录。<br>
使用镜像源很简单，用-i指定就行了： <br>
sudo easy_install -i http://pypi.douban.com/simple/ saltTesting <br>
sudo pip install -i http://pypi.douban.com/simple/ saltTesting<br>
把其设置为**默认源**：
```shell
1.linux 
    ~/.pip/pip.conf 
2.windows 
    %HOME%\pip\pip.ini 
添加：
[global] 
index-url = http://pypi.douban.com/simple
[install]
trusted-host = pypi.douban.com
```