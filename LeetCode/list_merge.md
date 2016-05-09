##21. Merge Two Sorted Lists   

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
###Solution
```C
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1)
            return l2;
        else if(!l2)
            return l1;
        ListNode *ret,*head;
        ret = head;
        while(l1&&l2)
        {
            if(l1->val>l2->val)
            {
                head->next=l2;
                head = head->next;
                l2=l2->next;
            }
            else
            {
                head->next=l1;
                head = head->next;
                l1=l1->next;
            }
        }
        if(l1)
            head->next = l1;
        if(l2)
            head->next = l2;
        return ret->next;
    }
};
```
###Lesson
* 
head 在两个链表上跑。
* 
有一个到结尾了，需要把另外一个链表连到最后

##88. Merge Sorted Array
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
###Solution
```C
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int>::iterator iter1,iter2,temp;
        iter1=nums1.begin();
        iter2=nums2.begin();
        for(;iter1!=nums1.end()&&iter2!=nums2.end();)
        {
            if(*iter1>*iter2)
            {
                temp = nums1.insert(iter1,*iter2);
                ++iter2;
                iter1=temp+1;
            }
            else
                ++iter1;
        }
        if(iter1==nums1.end())
            while(iter2!=nums2.end())
                nums1.push_back(*iter2++);
    }
};
//Better
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n)
{
    int i=m-1;
    int j=n-1;
    int k = m+n-1;
    while(i >=0 && j>=0)
    {
        if(nums1[i] > nums2[j])
            nums1[k--] = nums1[i--];
        else
            nums1[k--] = nums2[j--];
    }
    while(j>=0)
        nums1[k--] = nums2[j--];
}
```
###Lesson
* 
insert: 返回第一个插入成功的迭代器
* 
insert到中间：效率很低
* 
从后向前插入，

[返回目录](README.md)