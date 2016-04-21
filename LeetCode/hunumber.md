## Ugly Number

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.

###Solution
```C
class Solution {
public:
    bool isUgly(int num) {
        for(int i = 2;i<6&&num>1;++i)
            while(num%i==0)
                num/=i;
        return num==1;
    }
};
```
###Lesson
* 
把2 3 5 不断除后，如果等于1则说明是，否则不是

## Happy Number

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

```
Example: 19 is a happy number

12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```
###Solution
```C
bool isHappy(int num)
{
    int max = 1000;
    int s = 0,t = 0;
    while(max--)
    {
        while(num)
        {
            t = num%10;
            s += t*t;
            num /= 10;
            num = s;
            s = 0;
        }
        if(s==1)
            break;
    }
    if(s==1)
        return true;
    return false;
}
```
###Lesson
* 
max：代表当endless时，假设从2到最大平方和的可能，都出现一遍然后循环。这是最坏的可能，也就是说当endless时最多可以循环max次。（但此max是10个9的平方和，可能）