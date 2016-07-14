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
    uint32_t ig = n >> 1;
    uint32_t max = n, min = 0;
    int ret = guess(ig);
    while(ret != 0)
    {
        if(ret == 1)
        {
            min = ig;
            ig = (ig + max) >> 1;
        }
        else if(ret == -1)
        {
            max = ig;
            ig = (ig + min) >> 1;
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
相加可能出现超过最大范围，我们此处用的是uint32_t！！！相加除2超过范围解决方案：
    * 
用uint32_t（比较局限）
    * 
a + ((b-a) >>1)