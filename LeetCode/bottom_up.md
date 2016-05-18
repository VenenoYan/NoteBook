##107. Binary Tree Level Order Traversal II 

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).
```C
For example:
Given binary tree {3,9,20,#,#,15,7},
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]
```
###Solution
```C
vector<vector<int>> levelOrderBottom(TreeNode* root) {
    vector<vector<int>> ret;
    vector<int> inside;
    inside.clear();
    ret.clear();
    if(!root)
        return ret;
        
    queue<TreeNode*> s;
    int num = 0;
    int count = 1;
    s.push(root);
    while(!s.empty())
    {
        num = count;
        count=0;
        for(int st = 0;st<num;++st)
        {
            TreeNode *temp = s.front();
            s.pop();
            if(temp->left)
            {
                    s.push(temp->left);
                    ++count;
            }
            if(temp->right)
            {
                    s.push(temp->right);
                    ++count;
            }
            inside.push_back(temp->val);
        }
        ret.push_back(inside);
        inside.clear();
    }
    reverse(ret.begin(),ret.end());
    return ret;
}
```