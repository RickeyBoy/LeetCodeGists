### 142. 环形链表 II

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

 

示例 1：
```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

示例 2：
```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```

示例 3：
```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```

 

进阶：
你是否可以不用额外空间解决此题？


### 解法：双指针两次，快慢指针一次+同速指针一次

- A（快）B（慢）指针找到相交点
- A 从起点、B 从交点开始同速遍历，相交点为圆起点

简要证明：
1. B 走了 k 步，其中环内 m 步；A 走了 B 的两倍， 2k 步
1. 因为最终两个指针相遇：【2k - k = 环的整数倍】
3. 如果 A 从起点开始走，走到相遇点会走 【k-m】 步
3. 如果 B 从相遇点开始走，走到相遇点可以走【环的整数倍-m】 步
4. 所以这样最终两者第一次相遇一定在环的起点

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *first, *second; // 快，慢
        first = head;
        second = head;
        if(first==NULL) return NULL;
        // 第一次遍历，快慢
        do {
            if(first->next==NULL||first->next->next==NULL) {
                // 无环
                return NULL;
            }
            second = second -> next;
            first = first -> next -> next;
        } while (second!=first);
        // 第二次遍历，同速
        first = second;
        second = head;
        while (second!=first) {
            // 注意先 while 一次，避免 index==0 的情况
            second = second -> next;
            first = first -> next;
        }
        return first;
    }
};
```
