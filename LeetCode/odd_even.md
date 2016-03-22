## 328. Odd Even Linked List My Submissions Question

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity. <br>只是针对位置的奇偶

Example:
Given 1->2->3->4->5->NULL,
return 1->3->5->2->4->NULL.
### solution
```C++
    ListNode* oddEvenList(ListNode* head) {
        if((!head)||(!head->next)||(!head->next->next))
            return head;
        ListNode* odd = head;
        ListNode* p,*even;
        p=even=odd->next;
        while(even->next)
        {
            odd->next=even->next;
            odd=even->next;
            if(!odd->next)
                break;
            even->next=odd->next;
            even=odd->next;
        }
        even->next=NULL;
        odd->next=p;
        return head;
    }```
###lesson
* 
注意是位置奇偶
* 
特殊情况：0个、1个、2个
* 
当前指针是否有效