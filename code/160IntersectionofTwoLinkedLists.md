#### [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。

**进阶：**你能否设计一个时间复杂度 `O(m + n)` 、仅用 `O(1)` 内存的解决方案？

### 解法：计数遍历两次

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *endA, *endB;
        endA = headA;
        endB = headB;
        int countA = 0;
        int countB = 0;
        while(endA->next) { 
            endA = endA->next;
            countA ++;
        }
        while(endB->next) { 
            endB = endB->next; 
            countB ++;
        }
        if (endA!=endB) return NULL; // 不相交
        // 找交点
        endA = headA;
        while (countA>countB) {
            endA = endA->next;
            countA--;
        }
        endB = headB;
        while (countB>countA) {
            endB = endB->next;
            countB--;
        }
        while(endA!=endB) {
            endA = endA->next;
            endB = endB->next;
        }
        return endA;
    }
};
```