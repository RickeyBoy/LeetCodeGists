# LeetCode 二叉树

### 概述

|      | LeetCode                                                     | 方法            | 备注       |                                                              |
| ---- | ------------------------------------------------------------ | --------------- | ---------- | ------------------------------------------------------------ |
| 1    | [226. 翻转二叉树（简单）](https://leetcode-cn.com/problems/invert-binary-tree) | 递归            |            | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/226InvertBinaryTree.md) |
| 2    | 二叉树：前序(144)、中序(94)、后续(145)、层次遍历(102)        | 递归 and 栈辅助 | 【基础题】 |                                                              |
| 3    | [105. 从前序与中序遍历序列构造二叉树（中等）](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) | 递归            |            | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/105ConstructBinaryTreefromPreorderandInorderTraversal.md) |
| 4    | [106. 从中序与后序遍历序列构造二叉树（中等）](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/) | 递归            |            | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/106ConstructBinaryTreefromInorderandPostorderTraversal.md) |
| 5    | [889. 根据前序和后序遍历构造二叉树（中等）](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/) | 递归            |            | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/889ConstructBinaryTreefromPreorderandPostorderTraversal.md) |
| 6    | [236. 二叉树的最近公共祖先（中等）](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/) | 递归DFS         | 【重点题】 | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/236LowestCommonAncestorofaBinaryTree.md) |

### 遍历总结

- 前序：根→左→右，`stack *rights`
- 中序：左→根→右，`stack *mids`
- 后序：左→右→根（反转：根→右→左），`stack *mids`
- 层次遍历：`queue *nodes`

### （前序遍历 + 中序遍历）构建二叉树范例

- 步骤：

1. 找到根节点 index：中序遍历第一个，根据 val 找到对应前序遍历根节点 index
2. 找到根节点左右子树 index：前序遍历，依赖根节点划分
3. 构建根节点，递归调用 buildRoot

- 优化项：

1. 创建 map<int, int> idx，含义是：map[x] = x 对应的前序遍历 index。减少每次查找根节点 index 耗时
2. 结尾处 idx.clear();

```cpp
class Solution {
public:
    map<int, int> idx; // map[x] = x 对应的前序遍历 index
    TreeNode* buildRoot(vector<int>& preorder, vector<int>& inorder, int& pre_idx, int inleft, int inright) {
        if(inleft == inright) return NULL; // 终止条件
        int rootV = preorder[pre_idx]; 
        TreeNode* root = new TreeNode(rootV);
        int index = idx[rootV]; // 前序遍历 根节点 index
        pre_idx++;
        // 找到左右子树 index，并递归
        root->left = buildRoot(preorder, inorder, pre_idx, inleft, index);
        root->right = buildRoot(preorder, inorder, pre_idx, index + 1, inright);
        return root;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(preorder.size()==0) return NULL;
        for(int i=0;i<inorder.size();i++) idx[inorder[i]] = i;
        int pre_idx = 0;
        TreeNode* root = buildRoot(preorder, inorder, pre_idx, 0, inorder.size());
        idx.clear();
        return root;
    }
};
```

### X 序遍历的代码模板

##### Preorder Traversal 前序遍历

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        // 栈辅助
        stack<TreeNode*> rights;
        vector<int> results;
        TreeNode* current = root;
        while(current != NULL) {
            results.push_back(current->val);
            if(current->left!=NULL) {
                if(current->right!=NULL) rights.push(current->right);
                current = current->left;
            } else if(current->right!=NULL) {
                current = current->right;
            } else if(rights.size()>0) {
                current = rights.top();
                rights.pop();
            } else {
                current = NULL;
            }
        }
        return results;
    }
};
```

##### 中序遍历

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        // 利用栈辅助
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
                results.push_back(current->val);
                current = current->right;
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

##### Preorder Traversal 后序遍历

```cpp
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

##### 层次遍历

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        // 利用队列辅助
        queue<TreeNode*> nodes;
        vector<vector<int>> results;
        if(root) nodes.push(root);
        else return results;
        while(!nodes.empty()) {
            vector<int> row;
            int n = nodes.size();
            for(int i=0;i<n;i++) {
                TreeNode* first = nodes.front();
                nodes.pop();
                row.push_back(first->val);
                if(first->left) nodes.push(first->left);
                if(first->right) nodes.push(first->right);
            }
            results.push_back(row);
        }
        return results;
    }
};
```