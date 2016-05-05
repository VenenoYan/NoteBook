
## Nim Game  [easy]

There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones. <br>
每次可以拿走1~3个石头，拿走最后一个的胜利


**Code:**
```C++
class Solution {
public:
    bool canWinNim(int n) {
        if(n%4==0)
            return false;
        else 
            return true;
    }
};```


Lesson:
```C
只要保证在4或者4的倍数时不是我拿即可```

