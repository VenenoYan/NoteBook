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
* 
可以用减法： a-(-b)即可
* 
不能用加减法，那么就需要考虑位操作：
    * 
与操作：可以得到那个位相加有进位；
    * 
异或操作：可以得到相加不会进位的位；