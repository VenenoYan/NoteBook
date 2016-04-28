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
            if(prices[i]<min)
            {
                min=prices[i];
                max=prices[i];
                low = i;
            }
            else if(prices[i]>max)
            {
                max=prices[i];
                high = i;
                if(diff<max-min)
                    diff=max-min;
            }
        }
        cout<<low+1<<""<<high+1<<endl;
        return diff;
    }
};
```
###Lesson
* 
记录最小的，因为今天买肯定会赚。然后找最大的