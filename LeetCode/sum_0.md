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
        ret += n/5;
        n /= 5;
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


[返回目录](README.md)