### 2.Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

### 解法
思路很简单，依次遍历相加，需要一个 previous 记录进位。
需要注意：两者长度可能不同！
注意：`while(l1 || l2 || previous)`巧妙用法。
``` cpp
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode res(0), *head = &res;
        int previous = 0;
        while(l1 || l2 || previous) {
            int sum = (l1 ? l1->val : 0) + (l2 ? l2->val : 0) + previous;
            previous = sum/10;
            head->next = new ListNode(sum%10);
            head = head->next;
            if (l1) { l1 = l1->next; };
            if (l2) { l2 = l2->next; };
        }
        return res.next;
    }
};
```