### [236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。


### 解法：递归 DFS

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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root) return NULL;

        // 找到 p、q 就返回
        if (p->val == root->val) return p;
        if (q->val == root->val) return q;

        // 递归
        TreeNode *left = lowestCommonAncestor(root->left,p,q);
        TreeNode *right = lowestCommonAncestor(root->right,p,q);

        if (!left) {
            // 左子树没有 p 和 q
            return right;
        } else if (!right) {
            // 又子数没有 p 和 q
            return left;
        } else {
            // p、q 分别在两侧，说明自己就是
            return root;
        }

        return NULL;
    }
};
```
