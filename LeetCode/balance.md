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
    //更好的方法：从底向上遍历，减少height的调用
    int dfsHeight (TreeNode *root) {
        if (root == NULL) return 0;

        int leftHeight = dfsHeight (root -> left);
        if (leftHeight == -1) return -1;
        int rightHeight = dfsHeight (root -> right);
        if (rightHeight == -1) return -1;

        if (abs(leftHeight - rightHeight) > 1)  return -1;
        return max (leftHeight, rightHeight) + 1;
    }
    bool isBalanced(TreeNode *root) {
        return dfsHeight (root) != -1;
    }
```
###Lesson
* 
高度差不能超过1:必须知道左右子树的高度
* 
不超过1,同时左右子树的状态
* 
理解记住第二种从下向上的遍历方法

[返回目录](README.md)