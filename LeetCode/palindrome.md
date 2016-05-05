## 234. Palindrome Linked List My Submissions Question

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


##141.Linked List Cycle  
Given a linked list, determine if it has a cycle in it.

###Solution
```C
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head||head->next==NULL)
            return false;
        ListNode *f,*l;
        f = l = head;
        while(f&&l)
        {
            l = l->next;
            if(f->next)             //先看是否有效
                f = f->next->next;  //先移动后判断相遇
            else 
                return false;
            
            if(l==f)
                return true;
        }
        return false;
    }
};
```
###Lesson
1. 
单链表是有环？<br>
　　　两个指针，一个快一个慢，如果相遇就说明有环

1. 
先移动后判断是否相遇

##142. Linked List Cycle II 
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Note: Do not modify the linked list.
###Solution
```C
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if(!head)
            return head;
        ListNode *f,*l;
        f = l = head;
        while(f&&l)
        {
            l = l->next;
            if(f->next)             
                f = f->next->next;  
            else 
                return NULL;
            
            if(l==f)
                break;
        }
        if(f!=l)
            return NULL;
        else
        {
            while(head!=f)
            {
                head=head->next;
                f=f->next;
            }
        }
        return head;
    }
};
```
[返回目录](README.md)