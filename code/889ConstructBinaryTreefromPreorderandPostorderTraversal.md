#### [889. 根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)

返回与给定的前序和后序遍历匹配的任何二叉树。

 pre 和 post 遍历中的值是不同的正整数。

 

示例：

输入：pre = [1,2,4,5,3,6,7], post = [4,5,2,6,7,3,1]
输出：[1,2,3,4,5,6,7]

### 解法：递归

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
    // unordered_map<int, int> pre_map; // 记录 value 对应的 index
    // unordered_map<int, int> post_map; // 记录 value 对应的 index
    TreeNode* buildRoot(vector<int>& preorder, vector<int>& postorder, int preLeft, int preRight, int postLeft, int postRight) {
        printf("root = %d, preLeft %d, preRight %d, postLeft %d, postRight %d \n", preorder[preLeft], preLeft, preRight, postLeft, postRight);
        // 递归终止
        if (preLeft > preRight) return NULL;
        if (preLeft == preRight) return new TreeNode(preorder[preLeft]);
        // 根节点
        int rootVal = preorder[preLeft];
        TreeNode *root = new TreeNode(rootVal);
        // case1：当前 root 为叶子节点<不存在此情况，前面已经过滤>
        // 找到 rightChild 在 inOrder 中的位置
        int inChildRight = -1;
        for (int i=preLeft+1;i<=preRight;i++) {
            if (preorder[i]==postorder[postRight-1]) {
                inChildRight = i;
                break;
            }
        }
        // 左分支长度: inChildRight-preLeft-1
        // 递归
        root->left = buildRoot(preorder, postorder, preLeft+1, inChildRight-1, postLeft, postLeft+inChildRight-preLeft-2);
        root->right = buildRoot(preorder, postorder, inChildRight, preRight, postLeft+inChildRight-preLeft-1, postRight-1);
        return root;
    }
    TreeNode* constructFromPrePost(vector<int>& preorder, vector<int>& postorder) {
        return buildRoot(preorder, postorder, 0, preorder.size()-1, 0, postorder.size()-1);
    }
};
```
