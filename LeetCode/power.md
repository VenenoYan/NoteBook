##[power of 2](bitset.md)

###Lesson
* 
bit表示，如果是2的幂，那么bieset中有且仅有一个1
<hr>
##power of 3
Give an integer, write a function to determine if it is apower of three.

###Solution
```C
int max3power = 1162261467;
bool isPowerOfThree(int num)
{
    if(num<=0||n>pow(2,31)-1)
        return false;
    return max3power%n==0;
}
```
###Lesson
* 
在整数中，3的幂最大为1162261467。只要能被它整除的肯定是3的幂

<hr>
##power of 4
Give an integer(signed 32bits), write a function to determine if it is apower of four.

###Solution
```C
bool isPowerOfFour(int num)
{
    if(num<=0||n>pow(2,31)-1)
        return false;
    bitset<32> t(num);
    if(t.count()!=1)
        return false;
    else
    {
        for(int i = 1;i<31;i+=2)
            if(t[i])
                return false;
    }
    return true;
}
```
###Lesson
* 
bit表示，如果是4的幂，那么bieset中有且仅有一个1；同时注意是4的幂不是2的，2可以是任意一位，4必须是下标为奇数的为1才行。

[返回目录](README.md)