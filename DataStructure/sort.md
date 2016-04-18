排序分为两种：内部排序和外部排序

## 内部排序
1. 
冒泡排序：每次遍历一遍找最小/最大的放到序列的头/尾部。
```C
void maopao(int []a)
{
    for(int i = 0;i<a.length;++i)
    {
        for(int j = i;j<a.length;++j)
        {
            if(a[i]>a[j])
                swap(a[min],a[i]);
        }  //没找到一个就换，效率低：下面先找到最终的下标，然后只换一次即可
///////////////////////////////////////////////////////////////////
        min = i;
        for(int j = i+1;j<a.length;++j)
        {
            if(a[min]>a[j])
                min = j;
        }
        swap(a[min],a[i]);//先找到最终的下标，然后只换一次即可
    }
}
```

1. 
直接插入排序:向已经有序的序列中插入,需要后移操作；
```C
    void insertsort(int *a)
    {
        
    }
```
1. 
希尔排序(插入排序的一种)又叫增量排序：把所有元素根据增量距离分为几组，然后对组内进行直接插入排序；对下一个增量排序，最后增量为1即全体直接插入排序。即可
```C
void shellinsert(list &l, int k)
{
    for(int i = k;i<l.length;++i)
    {
        if(l[i]>l[i-k])
        {
            
        }
    }
}
void shellsort(list &l, int []dlta)
{
    for(int i = 0;i<dlta.length;++i)
        shellinsert(l,dlta[i]);
}
```

1. 
快速排序

1. 
简单选择排序

1. 
堆排序(选择排序的一种)

1. 
归并排序

1. 
基数排序


### 比较

### 总结

## 外部排序
1. 
多路平衡归并
1. 
最佳归并树
1. 
置换-选择