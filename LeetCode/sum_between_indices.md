
### Range Sum By Indices
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.
<br>
    求给定区域内元素之和<br>
Example:

```C++
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3```

### 
Solution

```C++
class NumArray {
public:
    NumArray(vector<int> &nums) {
        sum.push_back(0);
        int i=0;
        for(vector<int>::iterator iter=nums.begin();iter!=nums.end();++iter,++i){
            sum.push_back(*iter+sum.back());
        }
    }

    int sumRange(int i, int j) {
        if(i<0||j>sum.size()-1)
            return -1;
        return sum[j+1]-sum[i];
    }
private:
    vector<int> sum;
};```


### Lesson:

* 
create a vector to save sum between 0 and i
* 
set vector with sum