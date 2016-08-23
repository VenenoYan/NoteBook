##345. Reverse Vowels of a String 
Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede".
###Solution
```C
class Solution {
public:
    string reverseVowels(string s) {
        if(s.size()<2)
            return s;
        int l =0 ,h = s.size()-1;
        char temp;
        set<char> ss{'a','e','i','o','u','A','E','I','O','U'};
        while(l<h)
        {
            while(l<h&&ss.find(s[l])==ss.end())
                ++l;
            while(l<h&&ss.find(s[h])==ss.end())
                --h;
            swap(s[l],s[h]);
            ++l;--h;    //别忘了此处
        }
        return s;
    }
};
//使用set查找：数量比较少时效率不高
```
###Lesson
* 
前后双指针的应用

[返回目录](README.md)