@@ 234. Palindrome Linked List My Submissions Question

Given a singly linked list, determine if it is a palindrome.
###solution
```C++
    bool isPalindrome(ListNode* head) {
        if(!head||!head->next)
            return false;
        if(head==head->next)
            return true;
        ListNode* n=head->next;
        n=n->next;
        while(n&&n->next)
        {
            if(head==n)
                return true;
            head=head->next;
            n=n->next->next;
        }
        return false;
    }
```
### lesson
1. 
单链表是有环？<br>
　　　两个指针，一个快一个慢，如果相遇就说明有环
1. 
环的长度？<br>
　　　从相遇点出发，回到该点经历的节点数

1. 
环的链接点在哪？<br>
　　　**定理：相遇点到连接点的距离等于头指针到连接点的距离**
1. 
链表的长度？<br>
　　　头指针到相遇点的长度加上问题2的长度即可
