##110. Balanced Binary Tree
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
###Solution
```C
    int height(TreeNode *root)
    {
        if(!root)
            return 0;
        return height(root->left)>height(root->right)?height(root->left)+1:height(root->right)+1;
    }
    bool isBalanced(TreeNode* root) {
        if(!root)
            return true;
        int l = height(root->left);
        int r = height(root->right);
        return abs(l-r)<=1&&isBalanced(root->left)&&isBalanced(root->right);    //三个条件
    }
```
###Lesson
* 
高度差不能超过1:必须知道左右子树的高度
* 
不超过1,同时左右子树的状态

[返回目录](README.md)