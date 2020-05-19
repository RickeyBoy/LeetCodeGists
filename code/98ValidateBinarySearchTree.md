### 98. Validate Binary Search Tree

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含小于当前节点的数。
- 节点的右子树只包含大于当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。


示例 1:
```
输入:
    2
   / \
  1   3
输出: true
```
示例 2:
```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
```

### 解法

找到 current 的左子树最大值以及右子树最大值，验证 current 是否合法

前序遍历验证所有 current 是否合法

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
    // max value of left subtree
    int maxLeftBST(TreeNode* root) {
        TreeNode* node = root->left;
        while(node && node->right) {
            node = node->right;
        }
        return node->val;
    }
    // min value of right subtree
    int minRightBST(TreeNode* root) {
        TreeNode* node = root->right;
        while(node && node->left) {
            node = node->left;
        }
        return node->val;
    }
    bool checkValid(TreeNode* root) {
        if(root->left && maxLeftBST(root)>=root->val) {
            return false;
        }
        if(root->right && minRightBST(root)<=root->val) {
            return false;
        }
        return true;
    }
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> rights;
        TreeNode* current = root;
        while(current) {
            if(!checkValid(current)) return false;
            if(current->left) {
                if(current->right) {
                    if(!checkValid(current->right)) return false;
                }
                current = current->left;
            } else if(current->right) {
                current = current->right;
            } else if(rights.size()>0) {
                current = rights.top();
                rights.pop();
            } else {
                current = NULL;
            }
        }
        return true;
    }
};
```
