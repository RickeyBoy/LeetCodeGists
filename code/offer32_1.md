### [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

### 解法：层次遍历

``` cpp
class Solution {
public:
    vector<int> levelOrder(TreeNode* root) {
        queue<TreeNode*> nodes;
        vector<int> result;
        if (!root) return result;
        nodes.push(root);
        while(!nodes.empty()) {
            TreeNode* n = nodes.front();
            result.push_back(n->val);
            if (n->left) nodes.push(n->left);
            if (n->right) nodes.push(n->right);
            nodes.pop();
        }
        return result;
    }
};
```