### 129. Sum Root to Leaf Numbers

给定一个二叉树，它的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 1->2->3 代表数字 123。

计算从根到叶子节点生成的所有数字之和。

说明: 叶子节点是指没有子节点的节点。

示例 1:
```
输入: [1,2,3]
    1
   / \
  2   3
输出: 25
解释:
从根到叶子节点路径 1->2 代表数字 12.
从根到叶子节点路径 1->3 代表数字 13.
因此，数字总和 = 12 + 13 = 25.
```
示例 2:
```
输入: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
输出: 1026
解释:
从根到叶子节点路径 4->9->5 代表数字 495.
从根到叶子节点路径 4->9->1 代表数字 491.
从根到叶子节点路径 4->0 代表数字 40.
因此，数字总和 = 495 + 491 + 40 = 1026.
```

### 解法：栈实现 DFS

- 深度优先遍历 + 栈辅助遍历
- 用原来的树 cur -> val 表示到当前节点的路径和

```cpp
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        stack<TreeNode*> s;
        if(root==NULL) return 0;
        TreeNode* cur = root;
        int result = 0;
        while(cur) {
            if(cur->left&&cur->right) {
                cur->left->val += (cur->val)*10;
                cur->right->val += (cur->val)*10;
                s.push(cur->right);
                cur = cur->left;
            } else if (cur->left) {
                cur->left->val += (cur->val)*10;
                cur = cur->left;
            } else if (cur->right) {
                cur->right->val += (cur->val)*10;
                cur = cur->right;
            } else if (!s.empty()) {
                result += cur->val;
                cur = s.top();
                s.pop();
            } else {
                result += cur->val;
                cur = NULL;
            }
        }
        return result;
    }
};
```

### Swift 解法

Swift 中没有 Queue 的数据结构，只能自己实现，所以用每轮拷贝的方式比较方便（可以考虑双栈队列来模拟，但是最坏依旧需要额外 On 空间，且复杂）

| **实现方式**              | **时间复杂度** | **空间复杂度**         | **特点说明**                       |
| ------------------------- | -------------- | ---------------------- | ---------------------------------- |
| Array + removeFirst()     | O(n) 出队慢    | 原始空间               | 最容易写，但性能差                 |
| 每轮 temp 拷贝            | O(n) 出队快    | 每轮 O(n) 拷贝         | 多用于 BFS，代码结构清晰，但耗内存 |
| 双栈 Queue<T>（均摊出队） | 均摊 O(1) 出队 | 最坏 O(n) 空间（双栈） | 推荐使用，性能稳定，空间还算可控   |
|                           |                |                        |                                    |

```swift
class Solution {
    func sumNumbers(_ root: TreeNode?) -> Int {
        if root == nil { return 0 }
        var current: [(Int, TreeNode)] = []
        var result = 0
        current.append((root!.val, root!))
        while !current.isEmpty {
            var temp: [(Int, TreeNode)] = []
            current.forEach { (value, node) in
                if node.left == nil && node.right == nil {
                    // it's leaf
                    result += value
                }
                if node.left != nil {
                    temp.append((value*10+node.left!.val, node.left!))
                }
                if node.right != nil {
                    temp.append((value*10+node.right!.val, node.right!))
                }
            }
            current = temp
        }
        return result
    }
}
```

