### Binary Tree 二叉树


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
