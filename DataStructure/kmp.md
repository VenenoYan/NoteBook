#KMP 算法
```C
母串：abcabaaabaabcac
字串：abaabcac
```
###普通匹配：
* 
策略：
双指针，一个指向母串x，一个指向子串y：
    * 
如果下标对应的字符相等，则两个指针都自加1；
    * 
否则，指向字串的指针归0，即y=0，而指向母串的指针为x-y+1。即从母串上一轮匹配的地方加一继续重头匹配
* 
算法实现：
```C
int normal_search(string *s,string *t)
{
        int ret,i,j;
        i = j = 0;
        ret = -1;
        while(i <= s.size()-t.size())
        {
            if(s[i] == t[j])
            {
                if(j == t.size()-1)
                    ret = i - j;
                ++i;
                ++j;
            }
        }
}
```