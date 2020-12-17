### [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

难度简单713收藏分享切换为英文关闭提醒反馈

翻转一棵二叉树。

### 解法

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        queue<TreeNode*> nodes;
        if(root) nodes.push(root);
        else return root;
        while(!nodes.empty()) {
            int n = nodes.size();
            for(int i=0;i<n;i++) {
                TreeNode* first = nodes.front();
                nodes.pop();
                // 交换
                TreeNode *temp = first->left;
                first->left = first->right;
                first->right = temp;
                if(first->left) nodes.push(first->left);
                if(first->right) nodes.push(first->right);
            }
        }
        return root;
    }
};
```
