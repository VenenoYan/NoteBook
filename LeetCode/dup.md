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