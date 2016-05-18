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
##102. Binary Tree Level Order Traversal 

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
```C
For example:
Given binary tree {3,9,20,#,#,15,7},
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]```
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
    int num = 0;    //每次进入下一行前置为count
    int count = 1;  //动态记录每行的个数
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
    reverse(ret.begin(),ret.end()); //加为107,不加为102
    return ret;
}
```
###Lesson
* 
树的遍历：queue
* 数组长度：sizeof
* 
记录每行的个数

##111. Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
###Solution
```C
int minDepth(TreeNode* root) {
    if(!root)
        return 0;
        
    int depth = 1;
    queue<TreeNode*> q;
    TreeNode *temp;
    int num=0,count = 1;
    bool find = false;
    
    q.push(root);
    while(!find)
    {
        num = count;
        count=0;
        for(int k = 0;k<num;++k)
        {
            temp = q.front();
            q.pop();
            if((!temp->left)&&(!temp->right))
                find = true;
            if(temp->left)
            {
                q.push(temp->left);
                ++count;
            }
            if(temp->right)
            {
                q.push(temp->right);
                ++count;
            }
        }
        if(!find)
            ++depth;
    }
    return depth;
}
```

[返回目录](README.md)