
## Nim Game  [easy]

There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones. 


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
只要保证我不拿4或者4的倍数即可```