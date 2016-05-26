##349. Intersection of Two Arrays M

Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

Note:
Each element in the result must be unique.<br>
The result can be in any order.
###Solution
```C
vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    vector<int> ret;
    set<int> ret1;
    ret.clear();
    ret1.clear();
    if(!nums1.size()||!nums2.size())
        return ret;
    sort(nums1.begin(),nums1.end());
    sort(nums2.begin(),nums2.end());
    int i,j,k;
    int len1,len2;
    i = j = k = 0;
    len1 = nums1.size();
    len2 = nums2.size();
    for(i=0;i<len1&&k<len2;++i)
    {
        for(j = k;j<len2;++j)
        {
            while(nums2[j]<nums1[i]&&j<len2)
    	        ++j;
            if(j<len2&&nums2[j]==nums1[i])
    	    {
    	        ret1.insert(nums1[i]);
    	        k = j;
    	    }else if(nums2[j]>nums1[i])
            {
                if(j>0)
                    k = j-1;
	            break;
            }
            else
            {
                for(set<int>::iterator t = ret1.begin();t!=ret1.end();++t)
                    ret.push_back(*t);
                return ret;                
            }
        }
    }
    for(set<int>::iterator t = ret1.begin();t!=ret1.end();++t)
        ret.push_back(*t);
    return ret;
}
```

###Lesson
* 
使用k记录上次匹配的地址，下次从k开始匹配（有序）
* 
如果主动的大于被动比较的，则说明结束了。因为所有的值都比被动的大；
* 
如果主动的小于被动的，说明可以k = j-1;从被动的上一个开始；

##350. Intersection of Two Arrays II 

Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

Note:
* 
Each element in the result should appear as many times as it shows in both arrays.
* 
The result can be in any order.

Follow up:<br>
* 
What if the given array is already sorted? How would you optimize your algorithm?
* 
What if nums1's size is small compared to num2's size? Which algorithm is better?
* 
What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

###Solution
```C
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> ret;
        ret.clear();
        if(!nums1.size()||!nums2.size())
            return ret;
        sort(nums1.begin(),nums1.end());
        sort(nums2.begin(),nums2.end());
        int i,j,k;
        int len1,len2;
        i = j = k = 0;
        len1 = nums1.size();
        len2 = nums2.size();
        for(;i<len1&&k<len2;++i)
        {
            for(j = k;j<len2;++j)
            {
                while(nums2[j]<nums1[i]&&j<len2)
        	        ++j;
                if(j<len2&&nums2[j]==nums1[i])
        	    {
        	        ret.push_back(nums1[i]);
        	        k = ++j;
                    break;
        	    }else if(j==len2)
                {
                    return ret;
                }
                else
                    break;         
            }
        }
        return ret;
    }
```
###Lesson
* 
匹配到了，i和j都要向前走一步。========》这是要求，每个元素仅匹配一次
* 


[返回目录](README.md)