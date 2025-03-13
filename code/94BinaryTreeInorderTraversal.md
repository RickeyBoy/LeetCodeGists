### 94. Binary Tree Inorder Traversal

给定一个二叉树，返回它的中序 遍历。

示例:
```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
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
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode*> stacks;
        vector<int> result;
        TreeNode* cur = root;

        while(cur!=nullptr || !stacks.empty()) {
            if (cur != nullptr) {
                stacks.push(cur); // add current node to stacks
                cur = cur -> left; // first go to left
            } else {
                // if cur == nullptr, then start pop stacks
                cur = stacks.top();
                stacks.pop();
                result.push_back(cur->val);
                cur = cur -> right;
            }
        }
        return result;
    }
};
```
