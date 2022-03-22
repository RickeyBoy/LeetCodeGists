### [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

翻转一棵二叉树。

### 解法一：递归

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) {
				return root;
		}
		TreeNode* l1 = invertTree(root->left);
		TreeNode* r1 = invertTree(root->right);
		root->left = r1;
		root->right = l1;
		return root;
    }
};
```



### 解法二：层次遍历

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
