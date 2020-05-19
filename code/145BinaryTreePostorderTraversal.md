### 144. Binary Tree Preorder Traversal

给定一个二叉树，返回它的 后序 遍历。

示例:
```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
```
进阶: 递归算法很简单，你可以通过迭代算法完成吗？

### 解法：利用栈辅助

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
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*> mids;
        vector<int> results;
        TreeNode* current = root;
        while(current!=NULL) {
            if(current->left!=NULL) {
                mids.push(current);
                TreeNode* temp = current->left;
                current->left = NULL;
                current = temp;
            } else if(current->right!=NULL) {
                mids.push(current);
                TreeNode* temp = current->right;
                current->right = NULL;
                current = temp;
            } else if(mids.size()>0) {
                results.push_back(current->val);
                current = mids.top();
                mids.pop();
            } else {
                results.push_back(current->val);
                current = NULL;
            }
        }
        return results;
    }
};
```
