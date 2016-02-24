## 100. Same Tree
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.(两颗二叉树要结构同，值也要相同)

### **solution**
```C++
bool isSameTree(TreeNode* p, TreeNode* q) {
        bool ret1=true,ret2=true;
        if(q&&p){
            if(p->val!=q->val)
                return false;
            ret1=isSameTree(p->left,q->left);
            ret2=isSameTree(p->right,q->right);     //左右子树的返回值，留作判断
        }else if(!q&&!p)
            return true;
        else
            return false;
        return ret1&&ret2;
}
```
### **lesson**
1. 
树的遍历
1. 
节点同时为空时不是错
1. 
保留左右子树的返回值