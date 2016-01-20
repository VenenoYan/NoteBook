## Huffman树
**构造：**<br>
　　　1)在所有节点中选两个最小权值的节点来构建一个新的节点。这两个节点为新节点的左右子树。<br>
　　　2)然后删除这两个节点并把新节点加入到节点集中；<br>
　　　3)重复1)和2)过程，直至节点集没有节点了<br>
===============================<br>
　　　首先权值小的一定深度大。<br>
　　　整个过程共新建N-1个节点。该树2N-1个节点<br>
　　　整个Huffman树不存在度为1的节点（0/2）<br>
**代码实现：**
```C++
typedef struct HTNode
{
    char c;
    unsigned int weight;
    HTNode *parent,*lchild,*rchild;
    HTNode():c(' '),weight(0),parent(NULL),lchild(NULL),rchild(NULL){};
}；
void minum(HTNode *node,HTNode *head)
{
    HTNode *pre = head,*temp=head,*child=head;
    node = head;
    while(pre)
    {
        if(node->weight>pre->weight)
        {
            node = weight;
            child = temp;
        }
        temp = pre;
        pre = pre->parent;
    }
    if(node==head)
        head = head->parent;
    else
        child->parent = node->parent;
    
}
HTNode *HTCreate(const int *w, const char *s)
{
    int index=0;
    HTNode *head = new HTNode();
    while(w[index++])
    {
        HTNode *pres = new HTNode();
        pres->c=s[index];
        pres->weight=w[index];
        pres->parent = head;
        head = pres;
    }
    while(head->parent)
    {
        HTNode *m1 = new HTNode();
        HTNode *m2 = new HTNode();
        HTNode *newnode = new HTNode();
        minum(m1,head);
        minum(m2,head);
        newnode->weight=m1->weight+m2->weight;
        newnode->lchild=m1;
        newnode->rchild=m2;
        newnode->parent = head;
        m1->parent = newnode;
        m2->parent = newnode;
    }
}
```