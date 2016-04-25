
## Valid Anagram

Given two strings s and t, write a function to determine if t is an anagram of s.
<br>
比较两个字符串是否由相同的字符以相同的数量组成<br>
For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false. 


```C++
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        return s==t;
    }
};```

**Lesson:**

1、不管怎么样，排序好一定相同<br>
2、还可以用map统计出现次数  

<hr>
##20 .Valid Parentheses   
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
###Solution
```C
public:
    bool ispar(char s1,char s2)
    {
        switch (s1)
        {
            case '(':
                if(s2==')')
                    return true;
            case '{':
                if(s2=='}')
                    return true;
            case '[':
                if(s2==']')
                    return true;
            default:
                return false;
        }
            
    }
    bool isValid(string s) {
        if(s.size()==0)
            return true;
        else if(s.size()==1)
            return false;
        stack<char> st;
        int l = s.size()-1,i = 0;
        char is;
        while(i<=l)
        {
            if(st.empty())          //首先看是否空栈
                st.push(s[i++]);
            is= st.top();
            if(ispar(is,s[i]))
                st.pop();           //匹配弹出
            else
                st.push(s[i]);      //否则
            ++i;
        }
        if(st.empty())
            return true;
        return false;
    }
```
###Lesson
* 
栈保存
* 
首先判断栈是否为空：是先压入，然后判断：匹配弹出，否则压入
* 
下标的增加：空栈时，以及处理时