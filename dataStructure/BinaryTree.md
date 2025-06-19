# LeetCode 二叉树

### 概述

|      | LeetCode                                                     | 方法                  | 备注           |                                                              |
| ---- | ------------------------------------------------------------ | --------------------- | -------------- | ------------------------------------------------------------ |
| 1    | [226. 翻转二叉树（简单）](https://leetcode-cn.com/problems/invert-binary-tree) | 递归                  |                | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/226InvertBinaryTree.md) |
| 2    | 二叉树：前序(144)、中序(94)、后续(145)、层次遍历(102)        | 递归 and 栈辅助       | 【基础题】     |                                                              |
| 3    | [105. 从前序与中序遍历序列构造二叉树（中等）](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) | 递归                  |                | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/105ConstructBinaryTreefromPreorderandInorderTraversal.md) |
| 4    | [106. 从中序与后序遍历序列构造二叉树（中等）](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/) | 递归                  |                | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/106ConstructBinaryTreefromInorderandPostorderTraversal.md) |
| 5    | [889. 根据前序和后序遍历构造二叉树（中等）](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/) | 递归                  |                | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/889ConstructBinaryTreefromPreorderandPostorderTraversal.md) |
| 6    | [236. 二叉树的最近公共祖先（中等）](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/) | 递归DFS               | 【重点题】     | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/236LowestCommonAncestorofaBinaryTree.md) |
| 7    | [230. Kth Smallest Element in a BST](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/230KthSmallestElementinaBST.md) - medium | inorder traversal     | 【基础题】延伸 |                                                              |
| 8    | [199. Binary Tree Right Side View](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/199BinaryTreeRightSideView.md) - medium | level order traversal | 【基础题】延伸 |                                                              |

### X 序遍历的代码模板

##### Preorder Traversal 前序遍历

前序：根→左→右

核心思想：先输出 `val`，然后用 `stack` 依次存入 `right` 和 `left`

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> stk;
    if (root) stk.push(root);

    while (!stk.empty()) {
        TreeNode* node = stk.top(); stk.pop();
        res.push_back(node->val);
        if (node->right) stk.push(node->right); // 先右后左
        if (node->left) stk.push(node->left);
    }
    return res;
}
```

##### Inorder Traversal 中序遍历

中序：左→根→右，利用 curr 指针 + stack

核心思想：

1. 【左】先走到最左节点，存入过程中的节点，输出最左节点
2. 【根】从栈中取出节点，输出 val
3. 【右】开始处理这个节点的右节点（curr 指向其右节点）

```cpp
class Solution {
public:
  // 中序遍历：左 -> 根 -> 右（使用栈模拟递归过程）
  vector<int> inorderTraversal(TreeNode* root) {
      vector<int> res;
      stack<TreeNode*> stk;
      TreeNode* curr = root;

      while (curr != nullptr || !stk.empty()) {
          // 【左】一路向左走，直到最左节点
          while (curr != nullptr) {
              stk.push(curr);
              curr = curr->left;
          }
          // 【根】回退到上一个节点（左子树访问完毕）
          curr = stk.top();
        	stk.pop();
          res.push_back(curr->val);          // 记录当前节点
        	// 【右】继续访问右子树
          curr = curr->right;
      }
      return res;
  }
};
```

##### Preorder Traversal 后序遍历

后序：左→右→根

核心思想：将前序遍历改为（根→右→左），然后反转

```cpp
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> stk;
    if (root) stk.push(root);

    while (!stk.empty()) {
        TreeNode* node = stk.top(); stk.pop();
        res.push_back(node->val);
        if (node->left) stk.push(node->left); // 先左后右
        if (node->right) stk.push(node->right);
    }

    reverse(res.begin(), res.end()); // 反转得到左-右-根顺序
    return res;
}
```

##### 层次遍历

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        // 利用队列辅助
        queue<TreeNode*> nodes;
        vector<vector<int>> results; // 分层存储
        if(root) nodes.push(root);
        else return results;
        while(!nodes.empty()) {
            vector<int> row;
            int n = nodes.size();
            for(int i=0;i<n;i++) {
                TreeNode* first = nodes.front();
                nodes.pop();
                row.push_back(first->val);
	              // 遍历将下一层节点全部加入新数组
                if(first->left) nodes.push(first->left);
                if(first->right) nodes.push(first->right);
            }
            results.push_back(row);
        }
        return results;
    }
};
```

### LCA (Lowest Common Ancestor) 问题

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root) return NULL;
        // 找到 p、q 就返回
        if (p->val == root->val) return p;
        if (q->val == root->val) return q;
        // 递归
        TreeNode *left = lowestCommonAncestor(root->left,p,q);
        TreeNode *right = lowestCommonAncestor(root->right,p,q);
        if (!left) {
            // 左子树没有 p 和 q
            return right;
        } else if (!right) {
            // 又子数没有 p 和 q
            return left;
        } else {
            // p、q 分别在两侧，说明自己就是
            return root;
        }
        return NULL;
    }
};
```

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
