### 114. 二叉树展开为链表

给定一个二叉树，原地将它展开为一个单链表。

 

例如，给定二叉树
```
    1
   / \
  2   5
 / \   \
3   4   6
将其展开为：

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

### 解法：利用前序遍历

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        vector<TreeNode*> pres;
        pres = preorderTraversal(root);
        TreeNode *current = root;
        for (int i=1;i<pres.size();i++) {
            current -> right = pres[i];
            current -> left = NULL;
            current = pres[i];
        }
        return;
    }
    vector<TreeNode *> preorderTraversal(TreeNode* root) {
        // 栈辅助
        stack<TreeNode*> rights;
        vector<TreeNode*> results;
        TreeNode* current = root;
        while(current != NULL) {
            results.push_back(current);
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
