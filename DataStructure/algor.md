##1、递归算法
递归递归就是“递”和“归”的结合：
* 
递：不断传递，即划分子问题
* 
归：每个子问题找到结束的条件；或者继续处理

####1.1 模型
```C++
ret-type func(para)
{
    if(end_contion)
        return something;
    else
    {
        归纳处理普通条件即不结束的条件
        子问题
        调用自身
    }
    return something;
}
```
####1.2 例子
```C++
例如：返回一个二叉树的深度：
int depth(Tree t){ 
if(!t) return 0; 
else { 
         int a=depth(t.right); 
         int b=depth(t.left); 
         return (a>b)?(a+1):(b+1); 
    } 
}

判断一个二叉树是否平衡：
int isB(Tree t){ 
    if(!t) return 0; 
    int left=isB(t.left); 
    int right=isB(t.right); 
    if( left >=0 && right >=0 && left - right <= 1 || left -right >=-1) 
         return (left<right)? (right +1) : (left + 1); 
    else return -1; 
}
```
##2、动态规划
将待求解的问题分解成若干个相互联系的子问题，先求解子问题，然后从这些子问题的解得到原问题的解；对于重复出现的子问题，只在第一次遇到的时候对它进行求解，并把答案保存起来，让以后再次遇到时直接引用答案，不必重新求解。


[返回目录](README.md)