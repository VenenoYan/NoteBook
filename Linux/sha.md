##SHA
Secure Hash Algorithm (安全散列算法) 的缩写，它用来产生 20 个字节 (160位) 的散列值，该算法常用于数字签名，以防止数据遭到篡改。Linux下一般使用 openssl 提供 API 计算数据的 SHA1 值。
###例子
```C
#include <openssl/sha.h>
    unsigned char *SHA1(const unsigned char *d, unsigned long n,unsigned char *md);```

函数中的
* 
第 1 个参数 d 表示要处理的数据；
* 
第 2 个参数 n 表示该数据的长度；
* 
第 3 个参数 md 表示计算出的 sha 值的存放地方，如果为 NULL，那么系统会安排一个静态缓冲区对其存储。
```C++

```