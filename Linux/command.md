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
