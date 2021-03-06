## 191. Number of 1 Bits 

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

###solution
```C++
    int hammingWeight(uint32_t n) {
        bitset<32> hehe(n);
        return hehe.count();
    }
```
lesson:
```C++
bitset最好是无符号长整形
bitset<bits> name(string/unsigned long);
bitset<32> name(12); 即12的二进制位模式
bitset<32> name("1100"):注意读位顺序是相反的:0011

方法：
any()       存在为1的位吗
none()      不存在为1的位吗
count()     1的个数
size()      位数
test(pos)   测试pos是否为1
set()       所有位值为1
set(pos)    pos值设为1
reset()     所有设为0
reset(pos)  pos设为0
flip()      逐位取反
flip(pos)   pos取反
to_ulong()  按位返回一个unsigned long值
to_string() 按位返回一个string值,顺序一致
os<<b       输入至流中
```
## 231. Power of Two

Given an integer, write a function to determine if it is a power of two.
###solution
```C++
    bool isPowerOfTwo(int n) {
        if(n<=0)
            return false;
        bitset<32> t(n);
        return t.count()==1?true:false;
    }
    bool isPowerOfTwo(int n) {
        return (n>0&&(n&(n-1)==0));
    }
```
### Lesson

如果该数是2的幂，则对应的二进制中只有一个1。注意是负数或者是0.

## 190. Reverse Bits

Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).
###solution
```C++
    uint32_t reverseBits(uint32_t n) {
        bitset<32> t(n);
        bitset<32> tt;
        for(int i= 0 ;i<32;++i)
        {
            tt[i] = t[31-i];
        }
        return tt.to_ulong();
    }
```

[返回目录](README.md)