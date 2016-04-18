### 二叉排序树(BST)/二叉查找树：
```C
左孩子节点值比父节点小，而右孩子值比父大；每一个子节点都是一颗树。
查找算法：比当前小就进入左字树查找，大就进入右字树查找。
插入算法：比当前小就进入左字树插入，大就进入右字树插入。
typedef struct TreeNode
{
    int val;
    TreeNode *left,*right;
    TreeNode(){};
    TreeNode(int x):val(x),left(NULL),right(NULL){}
}TNode;
void insert(TNode *head,TNode *node)
{
    if(node->val>head->val)
    {
        if(head->right==NULL)
            head->right=node;
        else
            insert(head->right,node);
    }
    else
    {
        if(head->left==NULL)
            head->left=node;
        else
            insert(head->left,node);
    }
}
TreeNode *search(TNode *root, int v)
{
    if(root->val>v)
        return search(root->left,v)
    else if(root->val<v)
    {
        return search(root->child,v)
    }
    else if(root==v)
        return p;
    else
        return false;
}
TreeNode *create(int n)
{
    TNode *HT = new TreeNode(50);
    for(int i=0;i<n;++i)
    {
        TNode *NewNode = new TreeNode();
        NewNode->val = rand()%100;
        insert(HT,NewNode);
    }
    return HT;
}
```
删除时操作：
```
    删除节点类型：
    1)叶节点：直接删除，无影响
    2)只有一个子树：直接填上来
    3)有两个子树：在右子树的中序第一个节点拿上来填(”一提就可以了“：对应子树的变化)
```
![](IMG_20160116_105530.jpg)

### 平衡二叉树(AVL)：
保证每一个节点左右子树高度相差不超过1
```
```
![](IMG_20160116_105600.jpg)
![](IMG_20160116_105618.jpg)