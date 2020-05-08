### 572. 另一个树的子树

给定两个非空二叉树 s 和 t，检验 s 中是否包含和 t 具有相同结构和节点值的子树。s 的一个子树包括 s 的一个节点和这个节点的所有子孙。s 也可以看做它自身的一棵子树。

示例 1:
```
给定的树 s:

     3
    / \
   4   5
  / \
 1   2
给定的树 t：

   4 
  / \
 1   2
返回 true，因为 t 与 s 的一个子树拥有相同的结构和节点值。
```
示例 2:
```
给定的树 s：
     3
    / \
   4   5
  / \
 1   2
    /
   0
给定的树 t：
   4
  / \
 1   2
返回 false。
```


### 解法：暴力

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isSubtree(TreeNode* s, TreeNode* t) {
        stack<TreeNode*> rights;
        TreeNode* current = s;
        while(current != NULL) {
            if(isSametree(current,t)) return true;
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
        return false;
    }
    bool isSametree(TreeNode* s, TreeNode* t) {
        if (s==nullptr && t==nullptr) return true;
        else if (s==nullptr || t==nullptr) return false;
        else return s->val == t->val && isSametree(s->left,t->left) && isSametree(s->right,t->right);
    }
};
```
