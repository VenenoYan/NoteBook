
###  3Sum


Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.


#### Note:


Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)
The solution set must not contain duplicate triplets.
    For example, given array S = {-1 0 1 2 -1 -4},

    A solution set is:
    (-1, 0, 1)
    (-1, -1, 2)
    
### Code:

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int> > ret;
        vector<int> ca;
        vector<int>::iterator start,last;
        int sum=-1;
        
        if(nums.size()<3)
            return ret;
        sort(nums.begin(),nums.end());
        for(vector<int>::iterator iter1=nums.begin();iter1<(nums.end()-2);++iter1){
            start=iter1+1;
            last=nums.end()-1;
            while(start<last){
                sum=(*iter1+*start+*last);
                if(sum==0){
                    ca.clear();
                    ca.push_back(*iter1);
                    ca.push_back(*start);
                    ca.push_back(*last);
                    if(find(ret.begin(),ret.end(),ca)==ret.end()){
                        ret.push_back(ca);
                    }
                    ++start;
                    while(start<last&&*start==*(start-1)) ++start;
                    --last;
                    while(start<last&&*last==*(last+1)) --last;
                }else if(sum<0){
                    ++start;
                    while(start<last&&*start==*(start-1)) ++start;
                }
                else{
                    --last;
                    while(start<last&&*last==*(last+1)) --last;
                }
            }
            while(iter1!=(nums.end()-2)&&*iter1==*(iter1+1))
                ++iter1;
        }
        
        return ret;
    }
};```


### hint:

* 
no input
* 
all 0
* 
**many same values**
<br>

### Solved:

* 
    deal with it's length
* 
quick-sort
<br>

### Solution1: common version
```C++
void func1(vector<int> &data,vector<vector<int> > &res){
    for(vector<int>::iterator iter1=data.begin();iter1!=(data.end()-2);++iter1){
        for(vector<int>::iterator iter2=iter1+1;iter2!=(data.end()-1);++iter2){
            vector<int>::iterator iter3=iter2+1;
            while(iter3!=data.end()){
                if((*iter1+*iter2+*iter3)==0){
                    vector<int> one;
                    one.push_back(*iter1);
                    one.push_back(*iter2);
                    one.push_back(*iter3);
                    sort(one.begin(),one.end());
               
                    /* in case for duplication */
                    if(find(res.begin(),res.end(),one)==res.end()){
                        res.push_back(one);
                        vector<int>().swap(one);
                    }
                }
                ++iter3;
            }
        }
    }
}```


### Lesson:

1. 
sort firstly will help
1. 
quick-sort
* 
```vector<vector<int> >:need a space between '>',otherwise will be considered as '>>'```
* 
vector as param:    
```C++
        vector<int> tt;
        func(tt);    
        func(vector<int> &tes);```