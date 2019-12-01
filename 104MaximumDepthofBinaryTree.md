### 104. Maximum Depth of Binary Tree

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。


### 解法：层次遍历

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root) return 0;
        int h = 0;
        queue<TreeNode*> row;
        row.push(root);
        while(!row.empty()) {
            int n=row.size();
            for(int i=0;i<n;i++) {
                TreeNode* first = row.front();
                if(first->left) row.push(first->left);
                if(first->right) row.push(first->right);
                row.pop();
            }
            h++;
        }
        return h;
    }
};
```
