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
    
    //普通
    bool isSymmetric(TreeNode *root) {
        TreeNode *left, *right;
        if (!root)
            return true;
        
        queue<TreeNode*> q1, q2;
        q1.push(root->left);
        q2.push(root->right);
        while (!q1.empty() && !q2.empty()){
            left = q1.front();
            q1.pop();
            right = q2.front();
            q2.pop();
            if (NULL == left && NULL == right)
                continue;
            if (NULL == left || NULL == right)
                return false;
            if (left->val != right->val)
                return false;
            q1.push(left->left);
            q1.push(left->right);
            q2.push(right->right);
            q2.push(right->left);
        }
        return true;
    }
```
###Lesson
* 
树一般都可以递归调用
* 
普通：既然是相似，那么就用两个队列去统计左右子树