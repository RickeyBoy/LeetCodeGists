### 105. Construct Binary Tree from Preorder and Inorder Traversal

根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出
```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
```

### 解法：利用辅助函数递归

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
