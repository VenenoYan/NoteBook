##26. Remove Duplicates from Sorted Array   
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

把一个排好序的数组，删除重复的。返回剩下的长度
###Solution
```C
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        nums.erase(unique(nums.begin(),nums.end()),nums.end());
        return nums.size();
    }
};
```
##27. Remove Element
Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
Given input array nums = [3,2,2,3], val = 3

Your function should return length = 2, with the first two elements of nums being 2.

就是删除制定的元素
###Solution
```C
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        if(nums.size()==0)
            return 0;
        int i = 0, j = nums.size()-1;
        while(i<j)
        {
            while(nums[i]!=val&&i<j)
                ++i;
            while(nums[j]==val&&i<j)
                --j;
            swap(nums[i],nums[j]);
        }
        if(nums[i]==val)
            nums.erase(nums.begin()+i,nums.end());
        else if(nums[j]==val)
            nums.erase(nums.begin()+j,nums.end());
        else
            nums.erase(nums.begin()+j+1,nums.end());
        return nums.size();
    }
};
```
###Lesson
* 
特殊案例：[1]1--[2]3
## 217. Contains Duplicate.             
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

###solution
```C++
    bool containsDuplicate(vector<int>& nums) {
        set<int> dup;
        for(vector<int>::iterator t = nums.begin();t!=nums.end();++t){
            if(dup.count(*t))
                return true;
            dup.insert(*t);
        }
        return false;
    }```

### lesson
1. 
set.count(val): 出现次数统计<br>
set.find(val):  出现？本迭代器：end()


<hr>
## 169. Majority Element My Submissions Question

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

###solution
```C++
    int majorityElement(vector<int>& nums) {
        map<int,int> count;
        map<int,int>::iterator tt,max;
        for(vector<int>::iterator iter = nums.begin();iter!=nums.end();++iter){
            tt=count.find(*iter);
            if(tt==count.end()){
                count.insert(make_pair(*iter,1));
                if(count.size()==1)
                    max=count.begin();
            }else{
                ++tt->second;
                cout<<tt->second<<endl;
                if(tt->second>max->second)
                    max=tt;
            }
        }
        return max->first;
    }
```

### lesson
1. map的
1. 
**好的办法**：两个两个的比较，如果相等不处理，如果不相等删除这两个元素。那么最后剩下的那个元素肯定就是。但是注意刚开始两个就是相同的但他们不是majority。