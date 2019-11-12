### 19. Remove Nth Node From End of List

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：
```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？

### 解法：双指针

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *pre, *last;
        pre = head;
        last = head;
        for(int i=0;i<n;i++) {
            last = last -> next;
        }
        if(last==NULL) return head->next; // 注意边界条件
        while(last->next!=NULL) {
            pre = pre -> next;
            last = last -> next;
        }
        pre -> next = pre -> next -> next;
        return head;
    }
};
```