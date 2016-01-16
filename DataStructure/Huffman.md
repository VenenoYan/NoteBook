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
```C
typedef struct HTNode
{
    char c;
    unsigned int weight;
    HTNode *parent,*lchild,*rchild;
}
HTNode *HTCreate(int *w, char *s)
{
    int len=0,index=-1;
    while(w[len])
    {
        HTnode = (HTNode) malloc (sizeof(HTNode));
        HTnode->c=s[index];
        HTnode->weight=w[index];
        HTnode->parent=Null;
        HTnode->lchild = Null;
        HTnode->rchild = Null;
        ++len;
    }    
    while(--len!=1)
    {
        HTnodep = (HTNode) malloc (sizeof(HTNode));
        index = select_min(w);
        HTnode1 = (HTNode) malloc (sizeof(HTNode));
    //  HTnode1->c=s[index];
        HTnode1->weight=w[index];
        HTnode1->parent=Null;
        HTnode1->lchild = Null;
        HTnode1->rchild = Null;
        deletethis(index,w);
        deletethis(index,s);
        index = select_min(w);
        HTnode2 = (HTNode) malloc (sizeof(HTNode));
    //  HTnode2->c=s[index];
        HTnode2->weight=w[index];
        HTnode2->parent=Null;
        HTnode2->lchild = Null;
        HTnode2->rchild = Null;
        deletethis(index,w);
        deletethis(index,s);
        HTnodep->weight = HTnode1->weight+HTnode2->weight;
    }
}
```