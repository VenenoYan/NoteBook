
## 104. Maximum Depth of Binary Tree
Given a binary tree, find its maximum depth.求二叉树的深度

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
###solution
```C++
typedef struct TreeNode
{
    int val;
    TreeNode *left,*right;
    TreeNode(){};
    TreeNode(int x):val(x),left(NULL),right(NULL){}
}TNode;

int maxDepth(TNode *root)
{
    int depth = 0,num = 0,width = 1,count = 1;
    TNode *pre;
    queue<TNode *> que;
    if(!root)
        return 0;
    que.push(root);
    while(!que.empty())
    {
        num = 0;
        while(count--)
        {
            pre=que.front();
            if(pre->left)
            {
                que.push(pre->left);
                ++num;
            }
            if(pre->right)
            {
                que.push(pre->right);
                ++num;
            }
            que.pop();
        }
        cout<<endl;
        count = num;
        if(width<num)
            width = num;
        ++depth;
    }
    cout<<"width is "<<width<<"depth is "<<depth<<endl;
    return depth;
}```
###lesson
```C
用队列求高度和宽度。以层为单位压入
记录每一层即可。
```