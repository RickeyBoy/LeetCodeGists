### [100. 相同的树](https://leetcode-cn.com/problems/same-tree/)

给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

### 解法

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p==NULL && q==NULL) return true;
        else if (p==NULL || q==NULL) return false;
        else if (p->val != q->val) return false;
        else return isSameTree(p->left,q->left) && isSameTree(p->right,q->right);
    }
};
```
