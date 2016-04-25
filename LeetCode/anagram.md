
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
20 .Valid Parentheses   