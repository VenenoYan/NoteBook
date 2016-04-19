排序分为两种：内部排序和外部排序

## 内部排序
1. 
冒泡排序：相互比较，小的上浮。一遍只能找到一个
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
////////////////////////////////////////////////////////////////////////////////////////
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
直接插入排序：当前值与前一个比较，不符合顺序则替换，不断向前走，直至符合或者到达头。
```C
    void insertsort(int *a)
    {
        for(int i = 1; i< a.length();++i)
            for(int k = i;k>0&&a[k]<a[k-1];--k)
                swap(a[k],a[k-1]);
    }
```
1. 
希尔排序(插入排序的一种)又叫增量排序：把所有元素根据增量距离分为几组，然后对组内进行直接插入排序；对下一个增量进行希尔排序，最后增量为1即全体直接插入排序。即可
```C
void shellinsert(list &l, int k)
{
        for(int i = 0;i<k;++i)
        {
            for(int x = i+k;x<l.length;l+=k)
                for(int y = x;y>=k&&a[y]<a[y-k];y-=k)
                    swap(a[y],a[y-k]);
        }
}
void shellsort(list &l, int []dlta)
{
        for(int i = 0;i<dlta.length;++i)
            shellinsert(l,dlta[i]);
}
```

1. 
快速排序：一次排序后将待序的序列分为两个部分，一部分全是比关键字大的，另一部分小；然后分别对这两个部分快排。
```C
int partion(int *a,int low,int high)
{
        int p = a[low]
        while(low<high)
        {
            while(low<high&&a[high]>p)
                --high;
            a[low] = a[high];
            while(low<hihg&&a[low]<p)
                ++low;
            a[high]=a[low];
        }
        a[low]=p;
        return low;
}   //把比关键字大的和小的分开；
void quicksort(int *a,int low,int high)
{
        if(low<high)    //注意此处
            int pivot = partion(a,low,high);
        quicksort(a,low,pivot-1);
        quicksort(a,pivot+1,high);
}   //循环快排
void Qsort(int *a)
{
        int k= 0;
        while(a[k]) ++k;
        int low,high,mid;
        low = 0,high =k;
        quicksort(a,low,high);
}
```

1. 
简单选择排序：每次选择最小的和第一个的元素互换
```C
int selectmin(int *a,int start)
{
        int ret = start;
        for(int i = start+1;i<a.length;++i)
            if(a[ret]<a[i])
                ret= i;
        return ret;
}
void select(int *a)
{
        for(int i = 0;i<a.length;++i)
            {
                int index = selectmin(a,i);
                swap(a[i],a[index]);
            }
}
```

1. 
[堆排序](http://blog.csdn.net/morewindows/article/details/6709644)(选择排序的一种)：大小根堆，所有元素大于/小于根；
    * 
建立堆：
        * 
把数组保存的元素按完全二叉树建立：**第一个非终端节点是第floor(n/2)个**，调整以该节点为根节点的堆；
        * 
不断递减下标并重复上述操作到第一个元素
    * 
输出堆顶后调整：
        * 
输出堆顶元素，然后**把最后一个元素放到堆顶，自上向下调整堆。**
    * 
**插入堆：放到最后，自下向上调整（只需要调整直系亲属节点）；**

```C
/* 数组表示完全二叉树：第一个非终端节点是第floor(n/2)个元素，子节点下标：2i 、2i+1
// 只需要从floor(n/2)开始递增到1,判断每个节点的左右子树是否满足大小根要求即可。
*/
void heapinsert(int *a,int val) //放到最后啊！~！
{
    int l = 0;
    while(a[l]) ++l;
    a[l]=val;   //此处错误，仅为了表示需要
    for(int i = ceil(l/2)-1;i>=0;i=ceil(i/2)-1) //自下向上仅调整父亲
    {
        if(a[l]<a[i])
            swap(a[i],a[l]);
        l = i;
    }
}
void buildheap(int *a)
{
    int l = 0, mid;
    while(a[l]) ++l;
    mid = floor(l/2)-1;
    for(int i = mid;i>=0;--i)    //第一个非终端节点是第floor(n/2)个元素
    {
        if(a[2*i+2]>a[2*i+1])
            if(a[i]>a[2*i+1])
                swap(a[i],a[2*i+1]);
        else if(a[i]>a[2*i+2])
            swap(a[i],a[2*i+]);
    }
}
void adjheap(int *a)
{
    cout<<"the minum is: "<<a[0]<<endl;
    int l = 0;
    while(a[l]) ++l;
    a[0]=a[l-1];
    a[l-1]=NULL;    //此处仅表示拿掉一个元素，
    
}
void heapsort(int *a)
{
    int j= 0;
    while(a[j]) ++j;
    buildheap(a);
    for(int i=0;i<j;++i)
        adjheap(a);
}
```
7.归并排序

8.基数排序


### 比较

### 总结

## 外部排序
1. 
多路平衡归并
1. 
最佳归并树
1. 
置换-选择