###235. Lowest Common Ancestor of a Binary Search Tree
Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

 ``` 
        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```

For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

###Solution
```C++ 
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root->val > p->val && root->val > q->val)
            return lowestCommonAncestor(root->left,p,q);
        else if(root->val < p->val && root->val < q->val)
            return lowestCommonAncestor(root->right,p,q);
        else 
            return root;
    }
```
* 
此处方案：BST小的在左子树，大的在右子树；
    * 
如果root的值比两个都大，说明LCA在root的左子树上
    * 
如果root的值比两个都小，说明LCA在root的右子树上
    * 
如果一个大一个小或者相等，那么就说明root就是LCA

[返回目录](README.md)