### 101. Symmetric Tree

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
说明:

如果你可以运用递归和迭代两种方法解决这个问题，会很加分。
```

### 解法

按行遍历，每行进行验证。

注意空节点（null）在验证的时候也要进行比较

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
    bool isRowSymmetric(vector<TreeNode*> row) {
        int n = row.size();
        for(int i=0;i<n/2;i++) {
            TreeNode* left = row[i];
            TreeNode* right = row[n-i-1];
            if(left==NULL&&right==NULL) continue;
            else if(left!=NULL&&right!=NULL) {
                if(left->val == right->val) continue;
                else return false;
            } else {
                return false;
            }
        }
        return true;
    }
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        queue<TreeNode*> nodes;
        TreeNode* current = root;
        nodes.push(root);
        while(nodes.size()>0) {
            int n = nodes.size();
            vector<TreeNode*> row;
            for(int i=0;i<n;i++) {
                TreeNode* node = nodes.front();
                nodes.pop();
                if(node->left) nodes.push(node->left);
                if(node->right) nodes.push(node->right);
                row.push_back(node->left);
                row.push_back(node->right);
            }
            if(!isRowSymmetric(row)) return false;
        }
        return true;
    }
};
```
