
### 237. Delete Node in a Linked List

在一个链表中，删除一个节点。只提供该节点，而且你只能访问该节点。
```
Write a function to delete a node (except the tail) in a singly linked list, 
    given only access to that node.
Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, 
the linked list should become 1 -> 2 -> 4 after calling your function.```

### solution:

```C++
    void deleteNode(ListNode* node) {
        node->val=node->next->val;
        node->next=node->next->next;
    }```

### Lesson:

1. 复制下一个节点到自己身上，然后删除