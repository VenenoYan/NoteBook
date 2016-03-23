
### **237.** Delete Node in a Linked List

在一个链表中，删除一个节点。只提供该节点，而且你只能访问该节点。
```
Write a function to delete a node (except the tail) in a singly linked list, 
    given only access to that node.
Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, 
the linked list should become 1 -> 2 -> 4 after calling your function.```

### solution:

```C++
void deleteNode(ListNode* node) {
    if(node->next){
        node->val=node->next->val;
        node->next=node->next->next;
    }else
        node->next=NULL;
}```

### lesson:

1. 复制下一个节点到自己身上，然后删除下一个即可

<hr>

### **203**. Remove Linked List Elements

删除链表中指定的节点
```C
Remove all elements from a linked list of integers that have value val.

Example
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5```

### solution

```C++
ListNode* removeElements(ListNode* head, int val) {
    ListNode *start,*p;
    while(head&&head->val==val)
        head=head->next;
    p=start=head;
    while(start){
        if(start->val!=val){
            p=start;
            start=start->next;
        }
        else{
            p->next=start->next;
        }
    }
    return head;
}
```

### lesson


1. 使用上题的方法
1. 
没有使用：因为要放置一个哨兵，以防最后一个是要删除的;同时删除时更简单

## 19. Remove Nth Node From End of List My Submissions Question
```C++
Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
   ```
 ### solution
```C++
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(!head)     
            return head;
        ListNode* h,*ret;
        h=ret=head;
        while(n--) h=h->next;
        while(h&&h->next)
        {
            head=head->next;
            h=h->next;
        }
        if(!h)
            ret=ret->next;
        else
            head->next=head->next->next;
        return ret;
    }
```