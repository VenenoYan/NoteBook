##66. Plus One .
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

每一位代表以为数字：大端模式
###Solution
```C
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int len = digits.size()-1;
        for(int i = len;i>=0;--i)
        {
            if(digits[i]==9)
                digits[i] = 0;
            else
            {
                digits[i]++;
                return digits;
            }
        }
        digits.insert(digits.begin(),1);
        return digits;
    }
};
```
###Lesson
* 
大端：大的在低位。同正常感觉
* 
进位
* 
特殊：都是9,最后会多一位。