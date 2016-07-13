##371. Sum of Two Integers


Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:
Given a = 1 and b = 2, return 3. 
###Solution
```C++
class Solution {
public:
    int getSum(int a, int b) {
        int yi,yu;
        yu = a & b;
        yi = a ^ b;
        while(yu)
        {
            yu = yu << 1;
            a = yu;
            b = yi;
            yu = a & b;
            yi = a ^ b;
        }
        return yi;
    }
};
```
###Lesson
