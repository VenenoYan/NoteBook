##172 Factorial Trailing Zeroes
Given an integer n, return the number of trailing zeroes int n!;

就是给你一个数，求他阶乘法中末尾0的个数
###Solution
```C
int trailingZeroes(int n)
{
    if(n<5)
        return 0;
    int ret = 0;
    while(n>4)
    {
        ret += n/5;         //除5说明有几个5，那么至少这么多0(与任何一个偶数相乘即可)
        n /= 5;             //但是有些不止产生一个0，比如4*25，所以除5之后，继续
    }
    return ret;
}
//version：2
int trailingZeroes(int n)
{
    if(n < 5)
        return 0;
    else
    {
        int ret = 0;
        while(n >= 5)
        {
            ret += log10(n)/log10(5);
            n -= 5;
        }
        return ret;
    }
}
```
###Lesson
* 
结果末尾中有0,说明2和5相乘，或者乘以10;所以除5得到的值就是不满足第2条时0的个数
* 
如果\*2和\*5相乘的结果还有2与5,那么还要乘
* 
能除尽5,则说明一定有[*2]
* 
版本2：
    * 
换底公式：logcG = log10(G)/log10(c)
    * 
对5取对数，比如25得2，那么可以除尽5两次，那么就会有两个0；


[返回目录](README.md)