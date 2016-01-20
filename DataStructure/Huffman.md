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
HTNode *HTCreate(const int *w, const char *s)
{
    
}
```