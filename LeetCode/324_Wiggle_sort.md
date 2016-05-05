
### 324. Wiggle Sort II
Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....
<br>
把一个数组排序： 一个小于一个大于。。。。<br>
Example:<BR>
(1) Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6].<br>
(2) Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].<br>
Note:
You may assume all input has valid answer.<br>

**Solution**
```c++
void wiggleSort(vector<int>& nums) {
    sort(nums.begin(),nums.end());  
	int low1=0,low2=0;
	int index = nums.size()/2;
	if(nums.size()%2==0)
		low2=index;
	else
		low2=index+1;
	while(low2<nums.size()){
		nums.insert(nums.begin()+1+low1,nums[low2]);
		nums.erase(nums.begin()+low2+1);
		low1+=2;
		++low2;
	}
}//本题采用最简单的方法:排序，然后把后半部分大的插入到前面。注意插入后--相对位置的变化！
```

**Follow Up:**
Can you do it in O(n) time and/or in-place with O(1) extra space?

[返回目录](README.md)