##[power of 2](bitset.md)
##power of 3
Give an integer, write a function to determine if it is apower of three.

###Solution
```C
int max3power = 1162261467;
bool isPowerOfThree(int num)
{
    if(num<=0||n>pow(2,31)-1)
        return false;
    return max3power%n==0;
}
```