##206把单链表逆序  & 把单链表指定范围逆序
```C++
For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.```
####solution
```C++
//206
ListNode *reverseList(ListNode *head){
    if(!head)
        return NULL;
    ListNode *p,*q,*n;
    q=p=head;
    n=q->next;
    while(n){
        p->next=n->next;
        n->next=q;
        q=n;
        n=p->next;
    }
    return q;
}
//92
ListNode *reverseBetween(ListNode *head,int s,int e){
    if(!head||s==e)
        return head;
    ListNode *q,*p,*n;
    int diff = e-s;
    p = q = head;
    while(--s){
        q=p;
        p=p->next;
    }
    if(q==p){
        n=q->next;       //如果只有一个节点的话，那么s==e为True。早就结束了,即至少2个
        while(diff){
            q->next=n->next;
            n->next=p;
            p=n;
            n=q->next;
            --diff;
        }
        return p;
    }
    n=p->next;
    if(n==NULL){
        q->next=p->next;
        p->next=q;
        return p;
    }
    while(diff!=0){
        p->next=n->next;
        n->next=q->next;
        q->next=n;
        n=p->next;
        --diff;
    }
    return head;
}
```
####lesson
```C
1、头插入
2、指定时：
    1）从第一个1开始
    2) 哨兵
    3) 链表只有1、2个时的特殊处理
```

## 344 字符串逆序
```C
    string reverseString(string s) {
        if(s.size() <= 1)
            return s;
        int l = 0, h = s.size()-1;
        while(l<h)
        {
            swap(s[l],s[h]);
            ++l;
            --h;
        }
        //reverse(s.begin(),s.end());
        return s;
    }
```
###Lesson
* 
前后指针、快慢指针，本题使用前后指针。但这两种方法很有用！！
* 
当然本题还可以用栈解决，但是空间复杂度会比较高。

###190，Reverse Bits 
Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).
###Solution
```C++
    uint32_t reverseBits(uint32_t n) {
        uint32_t temp,ret,bit,la;
        temp = ret = bit = 0;
        la = 1;
        while(bit<32)
        {
            temp = la & n;
            if(temp != 0)
            {
                temp = pow(2,31-bit);
                ret += temp;
            }
            ++bit;
            la = pow(2,bit);
        }
        return ret;
    }
```

[返回目录](README.md)