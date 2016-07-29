## 101. Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

```
For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3

But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3```
###Solution
```C++
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        return issy(root->left,root->right);
    }
    bool issy(TreeNode* l,TreeNode* r)
    {
        if(!l||!r)
            return l == r;
        if(l->val != r->val)
            return false;
        return issy(l->left,r->right)&&issy(l->right,r->left);
    }
    
```