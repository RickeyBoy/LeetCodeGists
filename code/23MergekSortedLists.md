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

### 解法：利用 21 题（合并两个有序链表）进行归并

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

### 复杂度计算

k 个序列，总共 n 个数

时间复杂度：$O(nlogk)$

空间复杂度：$O(1)$






