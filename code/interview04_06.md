#### [面试题 04.06. 后继者](https://leetcode.cn/problems/successor-lcci/)

设计一个算法，找出二叉搜索树中指定节点的“下一个”节点（也即中序后继）。

如果指定节点没有对应的“下一个”节点，则返回`null`。

 

示例 1:
```
输入: root = [2,1,3], p = 1

  2
 / \
1   3

输出: 2
```
示例 2:
```
输入: root = [5,3,6,2,4,null,null,1], p = 6

      5
     / \
    3   6
   / \
  2   4
 /   
1

输出: null
```

### 解法：

``` cpp
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        TreeNode* fatherMin = NULL; // p 的所有父节点中的“下一个”
        TreeNode* sonMin = findMin(p->right); // p 的所有子节点中的“下一个”
        TreeNode* cur = root;
        while (cur->val != p->val) {
            // 遍历所有 p 的父节点
            if (cur->val < p->val) {
                cur = cur->right;
            } else {
                if (!fatherMin || cur->val < fatherMin->val) { fatherMin = cur; } // 更新 fatherMin
                cur = cur->left;
            }
        }
        // 只可能在父节点 or 子节点中
        if (fatherMin && sonMin) {
            return fatherMin->val < sonMin->val ? fatherMin : sonMin;
        } else if (fatherMin) {
            return fatherMin;
        } else {
            return sonMin;
        }
    }
    TreeNode* findMin(TreeNode* root) {
        while(root && root->left) {
            root = root -> left;
        }
        return root;
    }
};
```