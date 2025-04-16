### [199. Binary Tree Right Side View](https://leetcode.cn/problems/binary-tree-right-side-view/)

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return *the values of the nodes you can see ordered from top to bottom*.

 

**Example 1:**

**Input:** root = [1,2,3,null,5,null,4]

**Output:** [1,3,4]

**Explanation:**

![img](https://assets.leetcode.com/uploads/2024/11/24/tmpd5jn43fs-1.png)

**Example 2:**

**Input:** root = [1,2,3,4,null,null,null,5]

**Output:** [1,3,4,5]

**Explanation:**

![img](https://assets.leetcode.com/uploads/2024/11/24/tmpkpe40xeh-1.png)

**Example 3:**

**Input:** root = [1,null,3]

**Output:** [1,3]

**Example 4:**

**Input:** root = []

**Output:** []

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`



### 解法：**Level Order Traversal**

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
    vector<int> rightSideView(TreeNode* root) {
        queue<TreeNode*> q;
        vector<int> results;
        if (!root) return results; //edge case
        // init state
        q.push(root);
        // iteration
        while(!q.empty()) {
            int mostRightValue;
            int size = q.size();
            // go through the row
            for (int i=0;i<size;i++) {
                TreeNode* node = q.front();
                printf("%d ", node->val);
                q.pop();
                mostRightValue = node->val;
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            printf("\n");
            results.push_back(mostRightValue);
        }
        return results;
    }
};
```
