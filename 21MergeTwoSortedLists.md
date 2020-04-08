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
};
```


