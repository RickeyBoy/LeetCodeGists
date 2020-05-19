### 面试题18. 删除链表的节点

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

示例 1:
```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```
示例 2:
```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

说明：

* 题目保证链表中节点的值互不相同
* 若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点

### 解法：虚拟头节点

``` cpp
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val) {
        // 虚拟头节点
        ListNode *temp = new ListNode(0);
        temp->next = head;
        ListNode *cur = temp;
        while(cur && cur->next) {
            // 需要也判断 cur 存在的原因：最后一个了节点为被删除节点的时候
            if(cur->next->val==val) {
                cur->next = cur->next->next;
            }
            cur = cur->next;
        }
        return temp->next;
    }
};
```