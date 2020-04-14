### 面试题26. 树的子结构

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：
```
输入：A = [1,2,3], B = [3,1]
输出：false
```
示例 2：
```
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```
限制：
```
0 <= 节点个数 <= 10000.
```

### 解法：前序遍历 + 递归深搜

``` cpp
class Solution {
public:
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if(!A||!B) return false;
        // 前序遍历
        stack<TreeNode*> rights;
        TreeNode* current = A;
        while(current != NULL) {
            if(isSame(current,B)) return true; // 遍历时比较
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
    // 递归比较
    bool isSame(TreeNode* root, TreeNode* B) {
        if (B==NULL) return true;
        else if (root&&B) {
            return root->val == B->val && isSame(root->left,B->left) && isSame(root->right,B->right);
        } else {
            return false;
        }
    }
};
```