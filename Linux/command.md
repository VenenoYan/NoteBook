# 查看帮助：man command

5. linux下如何修改进程优先级？（nice命令的使用）。
6. linux下性能监控命令uptime介绍，平均负载的具体含义是什么？建议看server load概念。
7. 调试程序。bt显示栈信息，-g添加所有信息

查看cpu信息
cat /proc/cpiinfo

查看ubuntu版本:
cat /etc/issue

查看系统是32位还是64位
* 
方法1：
查看long的位数，返回32或64 getconf LONG_BIT
 
* 
方法2：
file /sbin/init


##linux用户

```C
    创建用户、设置密码、修改用户、删除用户：
useradd testuser 创建用户testuser
passwd testuser 给已创建的用户testuser设置密码,输入即可
    说明：新创建的用户会在/home下创建一个用户目录testuser
usermod --help 修改用户这个命令的相关参数
userdel testuser 删除用户testuser
rm -rf testuser 删除用户testuser所在目录
    用户组的添加和删除：
groupadd testgroup 组的添加
groupdel testgroup 组的删除

更改用户密码：passwd [usernam]
-k  保留即将过期的用户在期满后能仍能使用；
-d  删除用户密码，仅能以root权限操作；
-l  锁住用户无权更改其密码，仅能通过root权限操作；
-u  解除锁定；
-f  强制操作；仅root权限才能操作；
-x  两次密码修正的最大天数，后面接数字；仅能root权限操作；
-n  两次密码修改的最小天数，后面接数字，仅能root权限操作；
-w  在距多少天提醒用户修改密码；仅能root权限操作；
-i  在密码过期后多少天，用户被禁掉，仅能以root操作；
-S  查询用户的密码状态，仅能root用户操作；

```
##更新权限
```C++
chmod a+x
u stands for user.
g stands for group.
o stands for others.
a stands for all.


数字	说明	                                权限
0	没有任何权限	                            ---
1	执行权限	                                --x
2	写入权限	                                -w-
3	执行权限和写入权限：1 (执行) + 2 (写入) = 3	-wx
4	读取权限	                                r--
5	读取和执行权限：4 (读取) + 1 (执行) = 5	    r-x       
6	读取和写入权限：4 (读取) + 2 (写入) = 6	    rw-
7	所有权限: 4 (读取) + 2 (写入) + 1 (执行) = 7	rwx

-rw-r--r--：
从第二个字符起rw-是说用户bu有读、写权，没有运行权，接着的r--表示用户组users只有读权限，没有运行权，最后的r--指其他人（others）只有读权限，没有写权和运行权。
```
## ps: 终端下所有程序及进程
```C
ps a 显示现行终端机下的所有程序，包括其他用户的程序。
ps -A   显示所有程序。
ps c    列出程序时，显示每个程序真正的指令名称，而不包含路径，参数或常驻服务的标示。
ps -e  此参数的效果和指定"A"参数相同。
ps e   列出程序时，显示每个程序所使用的环境变量。
ps f    用ASCII字符显示树状结构，表达程序间的相互关系。
ps -H    显示树状结构，表示程序间的相互关系。
ps -N   显示所有的程序，除了执行ps指令终端机下的程序之外。
ps s     采用程序信号的格式显示程序状况。
ps S     列出程序时，包括已中断的子程序资料。
ps -t <终端机编号> 　指定终端机编号，并列出属于该终端机的程序的状况。
ps u 　 以用户为主的格式来显示程序状况。
ps x 　 显示所有程序，不以终端机来区分。
ps -l     較長,較詳細的顯示該PID的信息

最常用的方法是ps -aux,然后再利用一个管道符号导向到grep去查找特定的进程,然后再对特定的进程进行操作。


STATz状态位位常見的状态字符
D 无法中断的休眠状态（通常 IO 的进程）；
R 正在运行可中在队列中可过行的；
S 处于休眠状态；
T 停止或被追踪；
W 进入内存交换  （从内核2.6开始无效）；
X 死掉的进程   （基本很少見）；
Z 僵尸进程；
< 优先级高的进程
N 优先级较低的进程
L 有些页被锁进内存；
s 进程的领导者（在它之下有子进程）；
l 多进程的（使用 CLONE_THREAD, 类似 NPTL pthreads）；
+ 位于后台的进程组；
```
## top:实时显示系统中各个进程的资源占用状况


##[kill](http://www.cnblogs.com/peida/archive/2012/12/20/2825837.html):[终止](http://www.cnblogs.com/wangkangluo1/archive/2012/05/26/2518857.html)指定的进程
#### 杀死进程最安全的方法是单纯使用kill命令，不加修饰符，不带标志。 

```
root用户将影响用户的进程，非root用户只能影响自己的进程。
init进程是不可杀的

kill[参数][进程号]:
        发送指定的信号到相应进从而终结他们。不指定型号将发送SIGTERM（15）终止指定进程。
-l  信号，若果不加信号的编号参数，则“-l”参数会列出全部的信号名称
-a  当处理当前进程时，不限制命令名和进程号的对应关系
-p  指定kill 命令只打印相关进程的进程号，而不发送任何信号
-s  指定发送信号
-u  指定用户 

kill -l：列出所有的信号名称
kill -l [信号名称]：返回信号对应的数值

kill -2 123
kill -9 $(ps -ef | grep peidalinux) ：过滤出hnlinux用户进程并杀死
```
## grep：查找并打印
```linux
grep [-acinorvw] [--color=auto] '搜寻字符串' filename/*.*
        选项与参数：
        -a ：将 binary 文件以 text 文件的方式搜寻数据
        -c ：计算找到 '搜寻字符串' 的次数
        -i ：忽略大小写的不同，所以大小写视为相同
        -n ：顺便输出行号
        -o ：只显示正则表达式匹配的部分
        -r ：递归的读取目录下的所有文件，包括子目录。
        -v ：反向选择，亦即显示出没有 '搜寻字符串' 内容的那一行！
        -w ：精确匹配单词
        --color=auto ：可以将找到的关键词部分加上颜色的显示喔！
```
## ping：查看网络通路情况
* 
通信双方提前知道一些异常比如延迟、报文丢失等，就可以即使调整和控制，提供传输的效率和成功率。
* 
网际控制报文协议ICMP就是实现的该机制：主机或者路由发送ICMP报文来探测网络传输中的差错和异常。封装在IP数据包中
* 
ICMP分为两种：**差错报告报文和询问报文**
    * 
差错报文分为：终点不可达(3)、源点抑制(4)、时间超时(11)、参数问题(12)、改变路由(5)
    * 
询问报文分为：
        * 
回送请求(8)和回答(0)**<**源点向目地主机连续发送4条ICMP回送请求报文；目地主机接收到后会立即发送回送回答报文；源主机统计多少请求报文被发送、多少回答报文收到、往返时间、被丢弃多少报文等信息**>**
        * 
时间戳请求(13)和回答(14)：用于请求时间，做时间同步

##find：在目录结构中搜索文件，并执行指定的操作
**格式：find pathname [-para] [options]**
* 
pathname：路径。用.来表示当前目录，用/来表示系统根目录。 
* 
para：
    * 
-print：将结果输出到标准输出
    * 
-exec:对匹配的文件执行该参数所给出的shell命令
        * 
相应命令的形式为'command' {  } \;，注意{   }和\;之间的空格。 
    * 
-ok：与exec同，但每次都会让用户确认
* 
options:
```C
-name   按照文件名查找文件。
-perm   按照文件权限来查找文件。
-prune  不在当前指定的目录中查找，如果同时使用-depth选项，那么-prune将被find命令忽略。
-user   按照文件属主来查找文件。
-group  按照文件所属的组来查找文件。
-mtime -n +n  按照文件的更改时间来查找文件， 
        - n表示文件更改时间距现在n天以内，+n表示文件更改时间距现在n天以前。
-nogroup  查找无有效所属组的文件，即该文件所属的组在/etc/groups中不存在。
-nouser   查找无有效属主的文件，即该文件的属主在/etc/passwd中不存在。
-newer file1 ! file2  查找更改时间比文件file1新但比文件file2旧的文件。
-type  查找某一类型的文件，诸如：
        b - 块设备文件。
        d - 目录。
        c - 字符设备文件。
        p - 管道文件。
        l - 符号链接文件。
        f - 普通文件。
-size n：[c] 查找文件长度为n块的文件，带有c时表示文件长度以字节计。
-depth：在查找文件时，首先查找当前目录中的文件，然后再在其子目录中查找。
-fstype：查找位于某一类型文件系统中的文件
-mount：在查找文件时不跨越文件系统mount点。
-follow：如果find命令遇到符号链接文件，就跟踪至链接所指向的文件。
-cpio：对匹配的文件使用cpio命令，将这些文件备份到磁带设备中。
另外,下面三个的区别:
        -amin n   查找系统中最后N分钟访问的文件
        -atime n  查找系统中最后n*24小时访问的文件
        -cmin n   查找系统中最后N分钟被改变文件状态的文件
        -ctime n  查找系统中最后n*24小时被改变文件状态的文件
        -mmin n   查找系统中最后N分钟被改变文件数据的文件
        -mtime n  查找系统中最后n*24小时被改变文件数据的文件
```
* 
实例
    * 
find . -name "*.log"    ：当前目录下以log为后缀的所有文件
    * 
find /opt/soft/test/ -perm 777  ：权限为777的文件
    * 
find . -type f -name "*.log"    ：查找当目录，以.log结尾的普通文件
    * 
find . -name '*.html' -exec grep 'mailto:'{}：查找字符串
    * 
find . -size +1000000c -print 查找当前目录下大于1000000字节的文件 
    * 
find . -size+7M -print  查找大于7M 的文件

###netstat：查看网络服务
```C
-a (all)显示所有选项，默认不显示LISTEN相关
-t (tcp)仅显示tcp相关选项
-u (udp)仅显示udp相关选项
-n 拒绝显示别名，能显示数字的全部转化成数字。
-l 仅列出有在 Listen (监听) 的服务状态

-p 显示建立相关链接的程序名
-r 显示路由信息，路由表
-e 显示扩展信息，例如uid等
-s 按各个协议进行统计
-c 每隔一个固定时间，执行该netstat命令。

提示：LISTEN和LISTENING的状态只有用-a或者-l才能看到

找出运行在指定端口的进程： netstat -an | grep ':80'
lsof -i:#port       谁在使用#port

```
###lsof：显示系统打开的文件（linux一切都是文件）
```C
lsof语法格式是：
lsof ［options］ [filename]

lsof abc.txt 显示开启文件abc.txt的进程
lsof -c abc 显示abc进程现在打开的文件
lsof -c -p 1234 列出进程号为1234的进程所打开的文件
lsof -g gid 显示归属gid的进程情况
lsof +d /usr/local/ 显示目录下被进程开启的文件
lsof +D /usr/local/ 同上，但是会搜索目录下的目录，时间较长
lsof -d 4 显示使用fd为4的进程
lsof -i 用以显示符合条件的进程情况
lsof -i[46] [protocol][@hostname|hostaddr][:service|port]
  46 --> IPv4 or IPv6
  protocol --> TCP or UDP
  hostname --> Internet host name
  hostaddr --> IPv4地址
  service --> /etc/service中的 service name (可以不止一个)
  port --> 端口号 (可以不止一个)
 ```
###同步数据到硬盘：sync
###显示开机信息：dmesg
```C
dmesg [-cns]

补充说明：kernel会将开机信息存储在ring buffer中。您若是开机时来不及查看信息，可利用dmesg来查看。
开机信息亦保存在/var/log目录中，名称为dmesg的文件里。

参　　数：
　-c 　显示信息后，清除ring buffer中的内容。 
　-s    <缓冲区大小>预设置为8196，刚好等于ring buffer的大小。 
　-n 　设置记录信息的层级。
　
demsg | more/less/head/tail/grep str/-num...
```
###more、less、cat、head、tail
```C
cat：连接并显示文件
          -A, --show-all           等价于 -vET
          -b, --number-nonblank    对非空输出行编号
          -e                       等价于 -vE
          -E, --show-ends          在每行结束处显示 $
          -n, --number             对输出的所有行编号
          -s, --squeeze-blank      不输出多行空行
          -t                       与 -vT 等价
          -T, --show-tabs          将跳格字符显示为 ^I
          -u                       (被忽略)
          -v, --show-nonprinting   使用 ^ 和 M- 引用，除了 LFD 和 TAB 之外
          --help     显示此帮助信息并离开
          >/>> [filename]           新建文件或向文件添加内容
more：根据窗口的大小进行分页显示，然后还能提示文件的百分比；
        +num   从第num行开始显示；
        -num   定义屏幕大小，为num行；
        +/pattern   从pattern 前两行开始显示；
        -c   从顶部清屏然后显示；
        -d   提示Press space to continue, 'q' to quit.（按空格键继续，按q键退出），禁用响铃功能； 
        -l    忽略Ctrl+l （换页）字符；
        -p    通过清除窗口而不是滚屏来对文件进行换页。和-c参数有点相似；  
        -s    把连续的多个空行显示为一行；
        -u    把文件内容中的下划线去掉退出more的动作指令是q
    Enter       向下n行，需要定义，默认为1行；
    Ctrl+f    向下滚动一屏；
    空格键          向下滚动一屏；
    Ctrl+b  返回上一屏；
    =         输出当前行的行号；
    :f      输出文件名和当前行的行号；
    v      调用vi编辑器；
less：对文件或其它输出进行分页显示
        -c 从顶部（从上到下）刷新屏幕，并显示文件内容。而不是通过底部滚动完成刷新；
        -f 强制打开文件，二进制文件显示时，不提示警告；
        -i 搜索时忽略大小写；除非搜索串中包含大写字母；
        -I 搜索时忽略大小写，除非搜索串中包含小写字母；
        -m 显示读取文件的百分比；
        -M 显法读取文件的百分比、行号及总行数；
        -N 在每行前输出行号；
        -p pattern 搜索pattern；比如在/etc/profile搜索单词MAIL，就用 less -p MAIL /etc/profile
        -s 把连续多个空白行作为一个空白行显示；
        -Q 在终端下不响铃；
    回车键 向下移动一行；
    y 向上移动一行；
    空格键 向下滚动一屏；
    b 向上滚动一屏；
    d 向下滚动半屏；
    h less的帮助；
    u 向上洋动半屏；
    w 可以指定显示哪行开始显示，是从指定数字的下一行显示；比如指定的是6，那就从第7行显示；
    g 跳到第一行；
    G 跳到最后一行；
    p n% 跳到n%，比如 10%，也就是说比整个文件内容的10%处开始显示；
    /pattern 搜索pattern ，比如 /MAIL表示在文件中搜索MAIL单词；
    v 调用vi编辑器；
    q 退出less
    !command 调用SHELL，可以运行命令；比如!ls 显示当前列当前目录下的所有文件；
head：显示文件内容的前几行
    head -n 行数值 文件名；
tail：显示文件内容的最后几行
    tail -n 行数值 文件名；
```


[返回目录](README.md)