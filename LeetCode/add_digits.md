### Add Digits
```C
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit：
    给定整数各位相加，直至只有一位
For example:
Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it. ```

**Common solution:**
```C++
    int addDigits(int num) {
        int sum=0;
        while(num!=0){
            sum+=num%10;
            num/=10;
        }
        if(sum<10)
            return sum;
        else 
            return addDigits(sum);
        
    }```
    

### Without any loop/recursion in O(1)
```C++
int addDigits(int num) {
    return 1 + (num-1)%9; 
```

Lesson:
```C
对于一个非负整数，那么第一次的和一定小于100,即两位数------->不断对9取余```