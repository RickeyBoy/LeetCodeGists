# 莫里斯遍历

Morris Traversal 莫里斯遍历可以用 $O(n)$ 时间 $O(1)$ 空间进行二叉树三序遍历（不考虑输出数组的所占空间）。

相关的题目：
- [144. Binary Tree Preorder Traversal 二叉树的前序遍历](https://github.com/RickeyBoy/LeetCodeGists/blob/master/144BinaryTreePreorderTraversal.md)
- [94. Binary Tree Inorder Traversal 二叉树的中序遍历](https://github.com/RickeyBoy/LeetCodeGists/blob/master/94BinaryTreeInorderTraversal.md)
- [145. Binary Tree Postorder Traversal 二叉树的后序遍历](https://github.com/RickeyBoy/LeetCodeGists/blob/master/145BinaryTreePostorderTraversal.md)



### 核心思路：线索二叉树 + 问题等价

1. 原本的遍历需要使用 $O(n)$ 的栈辅助遍历
2. 二叉树的所有孩子节点均有空指针，所以一共有 2n+1 个空指针，利用这些空指针可以节省栈空间
3. 前序和中序比较简单，后序通过问题等价的方式映射成前序遍历。



### 构建线索：找到中序遍历时，根节点的前一个节点

也就是根节点左孩子的最右子节点：

```cpp
TreeNode* getLeftMostRight(TreeNode* root) {
    TreeNode* node = root->left;
    while(node!=NULL && node->right!=NULL && node->right!=root) {
        node = node->right;
    }
    return node;
}
```



### 前序：按逻辑迭代即可

对于某一时刻，遍历到某个节点 current，一共有三种情况：
- 无左分支：**将 current 加入结果**；开始遍历右分支
- 左分支被遍历过：将左分支线索清除，恢复树结构；开始遍历右分支
- 左分支未被遍历过：**将 current 加入结果**；标记左分支线索；开始遍历左分支



### 中序：与前序类似，只有加入 current 的时机略有不同

对于某一时刻，遍历到某个节点 current，一共有三种情况：
- 无左分支：**将 current 加入结果**；开始遍历右分支
- 左分支被遍历过：**将 current 加入结果**；将左分支线索清除，恢复树结构；开始遍历右分支
- 左分支未被遍历过：标记左分支线索；开始遍历左分支



### 后序：问题等价

后序遍历初次想起来比较复杂，但是我们可以通过等价的方式来思考，就很简单了。我们来跟前序来对比一下：

- 前序遍历：根 - 左 - 右
- 后序遍历：左 - 右 - 根



我们可以这样等价思考：

1. 将前序遍历算法直接左右反转，那么就是：根 - 右 - 左的遍历顺序。
2. 在遍历过程中，本来将节点值插入在队尾，现在直接插入在队头，相当于队列反转。那么就能得到：左 - 右 - 根的遍历顺序，也就是后序遍历。



所以我们可以按照这样的步骤来改写，就能得到后续遍历的代码：

1. 将前序遍历的代码中 left 和 right 完全互换。
2. 再将"插入队尾"的操作变成"插入队首"，即 `results.push_back(current->val)` 的替换为 `results.insert(results.begin(), current->val)`。



### 最终代码：前序

```cpp
class Solution {
public:
    TreeNode* getLeftMostRight(TreeNode* root) {
        TreeNode* node = root->left;
        while(node!=NULL && node->right!=NULL && node->right!=root) {
            node = node->right;
        }
        return node;
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> results;
        TreeNode* current = root;
        while(current!=NULL) {
            TreeNode* node = getLeftMostRight(current);
            if(node==NULL) {
                // 无左支
                results.push_back(current->val);
                current=current->right;
            } else if(node->right==current) {
                // 左支被遍历过了
                node->right = NULL;
                current=current->right;
            } else {
                // 未遍历过左支
                results.push_back(current->val);
                node->right = current;
                current = current->left;
            }
        }
        return results;
    }
};
```



### 最终代码：中序

```cpp
class Solution {
public:
    TreeNode* getLeftMostRight(TreeNode* root) {
        TreeNode* node = root->left;
        while(node!=NULL && node->right!=NULL && node->right!=root) {
            node = node->right;
        }
        return node;
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> results;
        TreeNode* current = root;
        while(current!=NULL) {
            TreeNode* node = getLeftMostRight(current);
            if(node==NULL) {
                // 无左支
                results.push_back(current->val);
                current=current->right;
            } else if(node->right==current) {
                // 左支被遍历过了
                results.push_back(current->val);
                node->right = NULL;
                current=current->right;
            } else {
                // 未遍历过左支
                node->right = current;
                current = current->left;
            }
        }
        return results;
    }
};
```



### 最终代码：后序

```cpp
class Solution {
public:
    // 翻转后的构建线索的方法
    TreeNode* getRightMostLeft(TreeNode* root) {
        TreeNode* node = root->right;
        while(node!=NULL && node->left!=NULL && node->left!=root) {
            node = node->left;
        }
        return node;
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> results;
        TreeNode* current = root;
        while(current!=NULL) {
            TreeNode* node = getRightMostLeft(current);
            if(node==NULL) {
                // 无右支
                results.insert(results.begin(), current->val); // 倒序插入
                current=current->left;
            } else if(node->left==current) {
                // 右支被遍历过了
                node->left = NULL;
                current=current->left;
            } else {
                // 未遍历过右支
                results.insert(results.begin(), current->val); // 倒序插入
                node->left = current;
                current = current->right;
            }
        }
        return results;
    }
};
```