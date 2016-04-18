#查找：
* 
####静态查找：只查找是否在表中
* 
####动态查找：增、删节点

#常用算法
###1. 折半查找
* 
思想：在有序表中查找，不断的折半！
* 
实现
```C++
int bin_search(SStable ST,keyType key)
{
    low = 1;high=ST.length;
    while(low<=high)
    {
        mid = (low+high)/2;
        if(ST[mid]<key)
            low = mid;
        else if(ST[mid]>key)
            high = mid;
        else
            return mid;
    }
}
```
* 
分析：在查找成功的情况下和判定树的深度有关：比较次数至多floor(log2(n))+1