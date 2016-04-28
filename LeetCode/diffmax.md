##121. Best Time to Buy and Sell Stock 
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

一天买找一天卖差额最大
###Solution
```C
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size()<=1)
            return 0;
        int diff = 0, min = prices[0] ,max= prices[0],low,high;
        low=high=0;         //记录结果的下标
        for(int i = 1 ; i<prices.size();++i)
        {
            if(prices[i]<min)   //遇到更小的
            {
                min=prices[i];
                max=prices[i];
                low = i;
            }
            else if(prices[i]>max)  //遇到更大的
            {
                max=prices[i];
                high = i;
                if(diff<max-min)    //新旧差距的比较
                    diff=max-min;
            }
        }
        cout<<low+1<<""<<high+1<<endl;
        return diff;
    }
};
case:
[]
[1]
[1,2,3,45]
[1,53523,4,34126]
[54,15423,6423144]
[45,231543,4,231540]
```
###Lesson
* 
记录最小的，因为今天买肯定会赚。然后找最大的。
* 
遇到更小的说明要以当前开始找：最后一个case
* 
遇到更大的，更新diff。
* 
diff记录当前最优解。