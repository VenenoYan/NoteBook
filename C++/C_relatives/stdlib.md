
## stdlib.h 头文件里包含了C语言的中最常用的系统函数

```C
宏：
NULL 空
EXIT_FAILURE 失败状态码
EXIT_SUCCESS 成功状态码
RAND_MAX rand的最大返回值
MB_CUR_MAX 多字节字符中的最大字节数

变量：
typedef size_t是unsigned integer类型
typedef wchar_t 一个宽字符的大小
struct div_t 是结构体类型 作为div函数的返回类型
struct ldiv_t是结构体类型 作为ldiv函数的返回类型

函数：

字符串函数
atof(); 将字符串转换成浮点型数
atoi(); 将字符串转换成整型数(第一个非空格字符是数字或者‘-’，否则为0,，之后检测到非数字(包括结束符\0)时停止转换
atol(); 将字符串转换成长整型数
strtod(); 将字符串转换成浮点数
strtol(); 将字符串转换成长整型数
strtoul(); 将字符串转换成无符号长整型数

内存控制函数
calloc(); 配置内存空间:自动初始化该内存空间为零，而malloc不初始化，里边数据是随机的垃圾数据。
free(); 释放原先配置的内存
malloc(); 配置内存空间(字节数):返回类型是 void*指向被分配内存的指针(此存储区中的初始值不确定)，否则返回空指针NULL
realloc(); 重新分配主存:新的大小小于原内存大小，可能会导致数据丢失，慎用！
        calloc比malloc 多了对内存的写零操作，而写零这个操作我们有时候需要，而大部分时间不需要
环境函数
abort(); 异常终止一个进程
atexit();设置程序正常结束前调用的函数
exit(); 正常结束进程
getenv(); 取得环境变量内容
system(); 执行shell 命令

搜索和排序函数
bsearch(); 二元搜索
qsort(); 利用快速排序法排列数组

数学函数
abs(); 计算整型数的绝对值
div(); 将两个整数相除, 返回商和余数
labs(); 取长整型绝对值
rand(); 随机数发生器
srand(); 设置随机数种子

多字节函数
mblen(); 根据locale的设置确定字符的字节数
mbstowcs(); 把多字节字符串转换为宽字符串
mbtowc(); 把多字节字符转换为宽字符
wcstombs(); 把宽字符串转换为多字节字符串
wctomb(); 把宽字符转换为多字节字符```