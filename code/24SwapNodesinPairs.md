#### 24. Swap Nodes in Pairs



给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。



你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。




示例:
```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```



### 解法

[RickeyBoy 的题解](https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/c-fei-di-gui-jie-fa-0ms-by-rickeyboy/)

创建虚拟头部，遍历

```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        // create a temp head ListNode
        ListNode *tempHead;
        tempHead = new ListNode(0);
        tempHead->next = head;
        auto pre = tempHead;
        auto last = tempHead;
        while(last->next&&last->next->next) {
            // move two steps
            last = last->next->next;
            // swipe two nodes
            pre->next->next = last->next;
            last->next = pre->next;
            pre->next = last;
            // NOTICE: need to last again
            last = last->next;
            pre = last;
        }
        // delete temp head
        pre = tempHead->next;
        delete tempHead;
        return pre;
    }
};
```



