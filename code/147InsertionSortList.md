### [147. 对链表进行插入排序](https://leetcode-cn.com/problems/insertion-sort-list/)

对链表进行插入排序。


示例 1：
```
输入:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
输出:
[
  "cats and dog",
  "cat sand dog"
]
```
示例 2：
```
输入:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
输出:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
解释: 注意你可以重复使用字典中的单词。
```
示例 3：
```
输入:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
输出:
[]
```


### 解法：$$O(n^2)$$ 暴力

```cpp
class Solution {
public:
    ListNode* insertionSortList(ListNode* head) {
        ListNode *fakeHead = new ListNode(INT_MIN); // 创造头节点
        fakeHead->next = head;
        ListNode *p = fakeHead; // 遍历到的点
        while (p && p->next) {
            ListNode *temp = fakeHead;
            ListNode *node = p->next; // 待替换的点
            bool needNext = true;
            while (temp!=node) {
                if (temp->val <= node->val && temp->next->val > node->val) {
                    // node 在 temp 和 temp->next 之间
                    p->next = node->next;
                    node->next = temp->next;
                    temp->next = node;
                    needNext = false;
                    break;
                } else {
                    temp = temp->next;
                }
            }
            // 没有进行插入
            if (needNext) {
                p = p->next;
            }
        }
        return fakeHead->next;
    }
};
```
