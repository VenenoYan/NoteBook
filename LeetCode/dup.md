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