### [103. 二叉树的锯齿形层序遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

给定一个二叉树，返回其节点值的锯齿形层序遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7   
```

返回锯齿形层序遍历如下：
```
[
  [3],
  [20,9],
  [15,7]
]
```

### 解法：按层遍历

```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> result;
        queue<TreeNode*> row;
        if (root) row.push(root);
        else return result;
        int isReverse = false;
        // each row
        while (row.size() > 0) {
            int k = row.size();
            vector<int> rowValue;
            for (int i=0;i<k;i++) {
                TreeNode *cur = row.front();
                row.pop();
                // value
                if (!isReverse) {
                    rowValue.push_back(cur->val);
                } else {
                    rowValue.insert(rowValue.begin(),cur->val);
                }
                // next row
                if (cur->left) row.push(cur->left);
                if (cur->right) row.push(cur->right);
            }
            result.push_back(rowValue);
            isReverse = !isReverse;
        }
        return result;
    }
};
```
