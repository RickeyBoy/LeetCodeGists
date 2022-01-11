# LeetCode 链表



### 概述

|      | LeetCode                                                     | 方法                                | 备注                 |                                                              |
| ---- | ------------------------------------------------------------ | ----------------------------------- | -------------------- | ------------------------------------------------------------ |
| 1    | [21. 合并两个有序链表（简单）](https://leetcode-cn.com/problems/merge-two-sorted-lists/) | while 遍历 + dummy                  |                      | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/21MergeTwoSortedLists.md) |
| 2    | [23. 合并K个升序链表（困难）](https://leetcode-cn.com/problems/merge-k-sorted-lists/) | 优先级队列（二叉堆） + dummy        | 【重点题】+ 求复杂度 | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/23MergekSortedLists.md) |
| 3    | [19. 删除链表的倒数第 N 个结点（中等）](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/) | 双指针，先走 N+1 步                 |                      | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/19RemoveNthNodeFromEndofList.md) |
| 4    | [876. 链表的中间结点（简单）](https://leetcode-cn.com/problems/middle-of-the-linked-list/) | 快慢指针                            |                      | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/876MiddleoftheLinkedList.md) |
| 5    | [141. 环形链表（简单）](https://leetcode-cn.com/problems/linked-list-cycle/) | 快慢指针                            |                      | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/141LinkedListCycle.md) |
| 6    | [142. 环形链表 II（中等）](https://leetcode-cn.com/problems/linked-list-cycle-ii/) | 快慢指针 + 链表起点                 |                      | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/142LinkedListCycleII.md) |
| 7    | [160. 相交链表（简单）](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/) | 计数遍历两次 or 首尾相连 + 环形链表 | 要求不改变环结构     | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/160IntersectionofTwoLinkedLists.md) |

### 技巧

- **「虚拟头结点」技巧，也就是 `dummy` 节点**。如果不使用 `dummy` 虚拟节点，代码会复杂很多，而有了 `dummy` 节点这个占位符，可以避免处理空指针的情况，降低代码的复杂性
- **优先级队列（二叉堆）**：快速找到最大/最小值

```cpp
// 声明方式
struct compare {
	bool operator()(ListNode* a, ListNode* b) {
		return a->val > b->val;
	}
};
priority_queue <ListNode*, vector<ListNode*>, compare> queue; // 小顶堆
```

- 环起点寻找方式

![rickey_4909](/Users/rickey/Desktop/Swift/LeetCodeGists/images/rickey_4909.png)



