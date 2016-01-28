Add Two Numbers

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8
### solution

```C++
//使用较长的那个链表返回
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode *h1=l1,*h2=l2,*head=NULL,*ret=NULL;
    int i1,i2,va,t=0;
    bool e(false);
    while(h1&&h2){
        h1=h1->next;
        h2=h2->next;
    }
    if(h1)
        head=l1;
    else
        head=l2;
    ret = head;
    while(l1||l2){
        i1=l1?l1->val:0;                        //三目运算符
        i2=l2?l2->val:0;
        va = (i1+i2+t)%10;
        t = (i1+i2+t)/10;
        if(t==0)
            e=false;                            //判断有没有进位，用于最后
        else
            e=true;
        head->val = va;
        head=head->next;
        if(l1&&l1->next)                        //结束条件
            l1=l1->next;
        else
            l1=NULL;
        if(l2&&l2->next)
            l2=l2->next;
        else
            l2=NULL;
    }
    head=ret;
    while(head->next)
        head=head->next;
    if(e){
        ListNode *ne=new ListNode(t);
        head->next=ne;
    }
    return ret;
}
```

### lesson

1. 
进位的判断
1. 
结束条件