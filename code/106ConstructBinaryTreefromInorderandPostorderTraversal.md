#### [106. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

根据一棵树的中序遍历与后序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

```
例如，给出
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
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
    TreeNode* buildRoot(vector<int>& inorder, vector<int>& postorder, int inLeft, int inRight, int postLeft, int postRight) {
        // 递归终止边界值
        if (inLeft > inRight) return NULL;
        if (inLeft == inRight) return new TreeNode(inorder[inLeft]);
        // 根节点值
        int rootVal = postorder[postRight];
        TreeNode *root = new TreeNode(rootVal);
        printf("root = %d, inLeft %d, inRight %d, postLeft %d, postRight %d \n", rootVal, inLeft, inRight, postLeft, postRight);
        // 找到根节点在 inOrder 中位置 (可以通过 map 优化)
        int inRoot = -1;
        for (int i=inLeft;i<=inRight;i++) {
            if (inorder[i]==rootVal) {
                inRoot = i;
                break;
            }
        }
        // 左分支部分大小: (inRoot-inLeft)
        // postOrder 中左支 [postLeft, postLeft + (inRoot-inLeft) - 1]
        // postOrder 中右支 [postLeft + (inRoot-inLeft), postRight -1]
        root->left = buildRoot(inorder, postorder, inLeft, inRoot-1, postLeft, postLeft + (inRoot-inLeft) - 1);
        root->right = buildRoot(inorder, postorder, inRoot+1, inRight, postLeft + (inRoot-inLeft), postRight-1);
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        return buildRoot(inorder,postorder,0,inorder.size()-1,0,postorder.size()-1);
    }
};
```
