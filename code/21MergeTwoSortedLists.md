### 21. Merge Two Sorted Lists

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

### 解法：虚拟头结点

注意读题、指针用法

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode *dummy = new ListNode(-1);
        ListNode *cur = dummy;
        while (list1 && list2) {
            if (list1->val < list2->val) {
                cur->next = list1;
                cur = cur -> next;
                list1 = list1->next;
            } else {
                cur->next = list2;
                cur = cur -> next;
                list2 = list2->next;
            }
        }
        if (list1) {
            cur->next = list1;
        }
        if (list2) {
            cur->next = list2;
        }
        return dummy->next;
    }
};
```

