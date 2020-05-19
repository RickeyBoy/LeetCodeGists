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

- AB快慢指针找到相交点
- A 从起点、B 从交点开始同速遍历，相交点为圆起点

简要证明：
1. 第一次相交点相遇，A 走了 x（环外）+ y（环内），B 走了 环的整数倍 - y
2. 当AB 一次走一步，走上次一样多的次数时，A 会和走的一样多；而 B 刚好走环的整数倍
3. 那么如果 A 从起点开始走，B 从相遇点开始走，那么 AB 还会在相遇点相遇
4. 因为相遇点在环上，所以 AB 这时首次相遇就是环的起点

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
