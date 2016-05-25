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