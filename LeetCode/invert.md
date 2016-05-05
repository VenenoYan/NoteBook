##Invert Binary Tree 

Invert a binary tree.

```     
     4
   /   \
  2     7
 / \   / \
1   3 6   9

to
     4
   /   \
  7     2
 / \   / \
9   6 3   1```
solution:
```C++
public:
    TreeNode* invertTree(TreeNode* root) {
        TreeNode *temp;
        if(root)
        {
            invertTree(root->left);
            invertTree(root->right);
            temp=root->left;
            root->left=root->right;
            root->right=temp;
        }
        return root;
    }```
lesson:
1. 
遍历，每个节点换一下左右兄弟即可

[返回目录](README.md)