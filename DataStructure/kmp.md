#KMP 算法
```C
母串：abcabaaabaabcac
字串：abaabcac
```
###普通匹配算法：
* 
策略：
双指针，一个指向母串x，一个指向子串y：
    * 
如果下标对应的字符相等，则两个指针都自加1即比较下一个字符是否相等；
    * 
否则，指向字串的指针归0，即y=0，而指向母串的指针x=x-y+1（此时x和y本轮自加的次数一定相等）。即从母串上一轮匹配的地方加一继续重头匹配
* 
算法实现：
```C
int normal_search(string *s,string *t)
{
        int ret,i,j;
        i = j = 0;
        ret = -1;
        while(i <= s.size()-t.size() && j != t.size())
        {
            if(s[i] == t[j])
            {
                ++i;
                ++j;
            }
            else
            {
                j = 0;
                i = x - j + 1;
            }
        }
        if( j == t.size() )
            ret = i - t.size();
        return ret;
}
```

##KMP算法
* 
策略：
    * 
我们从普通算法可知：如果当前匹配失败，那么字串从头匹配，母串下标为本轮开始匹配的地方加1即下一个字符；
    * 
KMP三个人分析，如下所示
```C
    母串S：  S0 S1 S2 S3 S4 ... Si-k Si-k+1 Si-j+2 ... Si-2 Si-1 Si ... Sx  ... Sn-2 Sn-1
    字串T：                     T0   T1     T2  . . .  Tk-2 Tk-1 Tj ... Tm-1
```
如果```Si != Sk```的话，按照普通算法，那么```k = 0; i = i - k + 1```，然后继续匹配；<br>
但是我们忽略了我们已经匹配过前k个了：即```【Si-k Si-k+1 Si-j+2 ... Si-2 Si-1】 = 【T0   T1     T2  . . .  Tk-2 Tk-1 】 ```
    * 
假若Si是我们字串成功匹配的范围之内，也就是说Si对应的字符在子串中即<br>```【Si-x Si-k+1 ... Si ... Si-x+m】 = 【T0   T1     T2  . . .  Tm-2 Tm-1 】```；那么一定存在一个j，使得：<br>```【Si-j Si-j+1 Si-j+2 ... Si-2 Si-1】 = 【T0   T1     T2  . . .  Tj-2 Tj-1 】```即Si前面的j个字符等于字串的后面j个字符（因为Si在匹配的范围内）

[返回目录](README.md)
