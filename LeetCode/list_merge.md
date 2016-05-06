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
};```