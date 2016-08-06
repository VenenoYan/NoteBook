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
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/sha.h>
　
#define SHA1LEN SHA_DIGEST_LENGTH
　
static const char hex_chars[] = "0123456789abcdef";
　
void convert_hex(unsigned char *md, unsigned char *mdstr)
{
    int i;
    int j = 0;
    unsigned int c;
    
    for (i = 0; i < 20; i++) {
        c = (md[i] >> 4) & 0x0f;
        mdstr[j++] = hex_chars[c];
        mdstr[j++] = hex_chars[md[i] & 0x0f];
    }
    mdstr[40] = '\0';
}
　
int main(int argc, char **argv)
{
    if (argc != 2) {
        fprintf (stderr, "usage: %s your-string\n", argv[0]);
        exit (EXIT_FAILURE);
    }
    
    char md[SHA_DIGEST_LENGTH];
    char mdstr[40];
    
    bzero(md, SHA_DIGEST_LENGTH);
    bzero(mdstr, 40);
    
    SHA1(argv[1], strlen(argv[1]), md);
    
    convert_hex(md, mdstr);
    
    printf ("Result of SHA1 : %s\n", mdstr);
    
    return 0;
}
Result of SHA1 : f6f80b59f1b25c82b64d857594fee53cd0df3604
```