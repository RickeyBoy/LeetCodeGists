#### [92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。

### 解法：头插法

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode *reverseBetween(ListNode *head, int left, int right) {
        ListNode *dummy = new ListNode(-1);
        ListNode *holdLeft;
        dummy->next = head;
        int count = 0;
        ListNode *cur = dummy;
        // 找到开始节点
        while (count<left) {
            if (count == left-1) {
                holdLeft = cur; // left-1 的位置
            }
            count++;
            cur = cur->next;
        }
        while (count<right) {
            ListNode *temp = holdLeft->next;
            holdLeft->next = cur->next;
            cur->next = holdLeft->next->next;
            holdLeft->next->next = temp;
            count++;
        }
        return dummy->next;
    }
};
```
