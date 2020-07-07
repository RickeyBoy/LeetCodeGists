### [112. 路径总和](https://leetcode-cn.com/problems/path-sum/)

给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

说明: 叶子节点是指没有子节点的节点。

示例: 
```
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2。
```

### 解法：利用前序遍历动态规划

```cpp
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        // 栈辅助前序遍历
        stack<TreeNode*> rights;
        TreeNode* current = root;
        while(current != NULL) {
            // 动态路径上的sum
            if (current->left!=NULL) {
                current->left->val += current->val;
            }
            if (current->right!=NULL) {
                current->right->val += current->val;
            }
            // 前序
            if(current->left!=NULL) {
                // 遍历左边
                if(current->right!=NULL) rights.push(current->right);
                current = current->left;
            } else if(current->right!=NULL) {
                // 遍历右
                current = current->right;
            } else {
                // 叶子节点
                if (current->val == sum) return true;
                else if(rights.size()>0) {
                    // 继续遍历
                    current = rights.top();
                    rights.pop();
                } else {
                    current = NULL;
                }
            }
        }
        return false;
    }
};
```
