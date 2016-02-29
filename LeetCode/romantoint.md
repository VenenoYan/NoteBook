## 13. Roman to Integer My Submissions Question         

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

### solution
```C++
    int ret(char s){
        switch(s){
            case 'I':
                return 1;
            case 'X':
                return 10;
            case 'C':
                return 100;
            case 'M':
                return 1000;
            case 'V':
                return 5;
            case 'L':
                return 50;
            case 'D':
                return 500;
        }
    }
    bool pro(char s1,char s2){
        if(ret(s1)-ret(s2)<0)
            return true;
        return false;
    }
    int romanToInt(string s) {
        int i=0,len=s.size(),p,q,sum=0;
        while(i<len-1){
            p=ret(s[i]);
            if(pro(s[i],s[i+1]))
                p*=(-1);
            sum+=p;
            ++i;
        }
        return sum+ret(s[len-1]);
    }
```

### Lesson
```
每位正常相加：
'I'：1
'X'：10;
'C': 100;
'M'：1000;
'V': 5;
'L': 50;
'D': 500;
数字上横线:1000倍
小的在大的:
    左边：小的为负
    右边：小的为正
```
## 12. Integer to Roman
Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.