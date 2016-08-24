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
        do{
            yi = a ^ b;
            yu = a & b << 1;
        }while(yu != 0);
        reutrn yi
    }
    int getSum(int a, int b) {
        if(a && b) 
            return getSum(a^b, (a&b) << 1);
        else 
            return a|b;
    }
};
```
###Lesson
* 
可以用减法： a-(-b)即可
* 
不能用加减法，那么就需要考虑**位操作**：
    * 
与操作：可以得到那个位相加有进位；结果就是进位值，同时左移一位既是进位的位置
    * 
异或操作：可以得到相加不会进位的位；
    * 
上述过程，与操作、异或操作的结果不断重复直到与操作没有进位即可；

[返回目录](README.md)