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
//顺序表：数组
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
分析：在查找成功的情况下和判定树的深度有关：比较次数至多 floor(log2(n))+1，平均：log2(n+1)-1

###2.分块查找、索引顺序查找
* 
思想：在顺序查找基础上建立一个索引表：对所有的元素分块，索引表就是对块的索引，记录块号起始位置和块中最大关键字，先在索引表中找块号，然后在该块中查找即可！

###3.[二叉排序、二叉平衡](BST.md)