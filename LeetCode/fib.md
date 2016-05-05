## 70. Climbing Stairs 
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
###Solution
```C
class Solution {
public:
    int climbStairs(int n) {
        if(n==0)
            return 1;
        else if(n==1)
            return 1;
        else if(n==2)
            return 2;
        else
        {
            int t1 = 1 , t2 = 2 , sum = 0;
            for(int i = 3 ; i <= n ; ++i)
            {
                sum = t1+t2;
                t1 = t2;
                t2 = sum ;
            }
            return sum;
        }
    }
};
```
###Lesson
* 
斐波纳契数列
* 
**注意：**动态规划不要用递归实现！超时还不好。

