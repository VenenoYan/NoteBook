### 374. Guess Number Higher or Lower
We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number is higher or lower.
```C
You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):
-1 : My number is lower
 1 : My number is higher
 0 : Congrats! You got it!

Example:

n = 10, I pick 6.

Return 6.
```
###Solution
```C++
int guessNumber(int n) {
    if(n == 1 || guess(n) == 0) 
        return n;
    uint32_t max = n, min = 0;
    while(ret != 0)
    {
        uint32_t ig = min + (max + min) >> 1;
        int ret = guess(ig);
        if(ret == 1)
        {
            min = ig;
        }
        else if(ret == -1)
        {
            max = ig;
        }
        ret = guess(ig);
    }
    return ig;
}
```
###Lesson
* 
上限、下限不断变化！！！
* 
相加可能出现超过最大范围，我们此处用的是uint32_t！！！相加除2，相加超过范围解决方案：
    * 
用uint32_t（比较局限）
    * 
a + ((b-a) >>1)

###278. First Bad Version

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API. 
###Solution
```C++
    int firstBadVersion(int n) {
        if(isBadVersion(1))
            return 1;
        uint32_t l = 1, h = n;
        uint32_t ig = n >> 1;
        bool ret = isBadVersion(ig);
        while(h - l != 1)
        {
        	cout<<l<<" "<<h<<" "<<ig<<endl;
            if(ret)
            {
                h = ig;
                ig = (ig + l) >> 1;
            }
            else
            {
                l = ig;
                ig = (ig + h) >> 1;
            }
            ret = isBadVersion(ig);
        }
        return h;
    }
```
###Lesson
* 
找值：截半法。
* 
注意第一个就是无效

[返回目录](README.md)