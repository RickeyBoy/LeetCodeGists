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

```cpp
class Solution {
public:
    map<int, int> idx;
    TreeNode* buildRoot(vector<int>& preorder, vector<int>& inorder, int& pre_idx, int inleft, int inright) {
        if(inleft == inright) return NULL;
        int rootV = preorder[pre_idx];
        TreeNode* root = new TreeNode(rootV);
        int index = idx[rootV];
        pre_idx++;
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
