##198. House Robber
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

就是说一个小区，你去偷钱。但是相连的两个都被偷就会触发警报，你被抓。怎么得到最多？最多多少？
###Solution
```C++
    public int rob(int[] num) {
        int i = 0;
        int e = 0;
        for (int k = 0; k<num.length; k++) {
            int tmp = i;
            i = num[k] + e;
            e = Math.max(tmp, e);
            
            //或者
            if (k%2==0)
            {
                i = max(i+num[k], e);
            }
            else
            {
                e = max(i, e+num[k]);
            }
        }
        return Math.max(i,e);
    }
```

###Lesson
* 
基准：
    ```C
    f(0) = nums[0]
    f(1) = max(num[0], num[1])
    f(k) = max( f(k-2) + nums[k], f(k-1) )
    ```