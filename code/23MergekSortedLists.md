### 23. Merge k Sorted Lists

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:
```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

### 解法一：利用 21 题（合并两个有序链表）进行归并

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode result(0), *current = &result;
        while(l1 && l2) {
            if(l1->val > l2->val) {
                current->next = new ListNode(l2->val);
                l2=l2->next;
                current=current->next;
            } else {
                current->next = new ListNode(l1->val);
                l1=l1->next;
                current=current->next;
            }
        }
        current->next = l1 ? l1 : l2;
        return result.next;
    }
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        int n = lists.size();
        if (n==0) return NULL;
        int interval = 1;
        while (interval < n) {
            for (int i=0;i<n-interval;i=i+interval*2) {
                lists[i] = mergeTwoLists(lists[i], lists[i+interval]);
            }
            interval = interval*2;
        }
        return lists[0];
    }
};
```

#### 复杂度计算

k 个序列，总共 n 个数

时间复杂度：$O(nlogk)$

空间复杂度：$O(1)$

### 解法二：利用优先级队列（小顶堆）

```cpp
class Solution {
public:
    struct compare {
        bool operator()(ListNode* a, ListNode* b) {
            return a->val > b->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue <ListNode*, vector<ListNode*>, compare> queue; // 小顶堆
        // 初始化
        for (ListNode *head : lists) {
            if (head) {
                queue.push(head);
            }
        }
        ListNode *dummy = new ListNode(-1);
        ListNode *cur = dummy;
        // 逐步添加
        while (!queue.empty()) {
            // 添加最小值
            cur->next = queue.top();
            queue.pop();
            cur = cur->next; // 此时也 cur == queue.top()
            printf("%d ", cur->val);
            // 添加下一个数
            if (cur->next) {
                queue.push(cur->next);
            }
        }
        // 结果
        return dummy->next;
    }
};
```

#### 复杂度计算

优先队列中的元素个数最多是 `k`，所以一次 `poll` 或者 `add` 方法的时间复杂度是 `O(logk)`；

所有的链表节点都会被加入和弹出 `pq`，**所以算法整体的时间复杂度是 `O(Nlogk)`，其中 `k` 是链表的条数，`N` 是这些链表的节点总数**。
