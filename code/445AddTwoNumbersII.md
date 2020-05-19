### 445. 两数相加 II

给你两个 非空 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

 

进阶：

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

 

示例：
```
输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7
```

### 解法1：栈

逆序应该首先想到用栈

```cpp

```

### 解法2：先反转链表

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *cur1 = reverse(l1);
        ListNode *cur2 = reverse(l2);
        int adder = 0;
        ListNode *cur, *result;
        while(cur1 || cur2 || adder > 0) {
            // 加数
            int i1 = cur1 ? cur1->val : 0;
            int i2 = cur2 ? cur2->val : 0;
            int i3 = adder;
            // 处理结果
            cur = result;
            result = new ListNode((i1+i2+i3)%10);
            result -> next = cur;
            adder = (i1+i2+i3)/10;
            // next
            if(cur1) cur1 = cur1->next;
            if(cur2) cur2 = cur2->next;
        }
        return result;
    }
    // 反转链表
    ListNode* reverse(ListNode* l) {
        ListNode *cur = l, *result = NULL;
        while(cur) {
            ListNode *temp = cur->next;
            cur->next = result;
            result = cur;
            cur = temp;
        }
        return result;
    }
};
```