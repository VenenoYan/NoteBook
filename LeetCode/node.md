
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