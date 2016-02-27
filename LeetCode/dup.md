## 217. Contains Duplicate.  　　　  169. Majority Element
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