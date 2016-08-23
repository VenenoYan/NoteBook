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
class Solution {
public:
    bool isvol(char c)
    {
        if(c=='a'||c=='A'||c=='e'||c=='E'||c=='i'||c=='I'||c=='o'||c=='O'||c=='u'||c=='U')
            return true;
        else
            return false;
    }
    string reverseVowels(string s) {
        size_t len = s.size();
        if(len <= 1)
            return s;
        int i,j;
        i = 0;
        j = len - 1;
        while(i < j)
        {
            while(i < j && !isvol(s[i]))
                ++i;
            while(i < j && !isvol(s[j]))
                --j;
            swap(s[i],s[j]);
            ++i;
            --j;
        }
        return s;
    }
};
```
###Lesson
* 
前后双指针的应用

[返回目录](README.md)