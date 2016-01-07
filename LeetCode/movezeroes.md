
## Move Zeroes

 Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0]. 
```C++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int len=0;
        for(vector<int>::iterator iter=nums.begin();iter!=nums.end();){
            if(*iter==0){
                nums.erase(iter);
                ++len;
                continue;
            }else
                ++iter;
        }
        while(len--)
            nums.push_back(0);
    }
};```

**Lesson**

1、vector的erase()方法，删除后，迭代器指向删除的下一个元素
2、push_back()方法，添加后，end()加1