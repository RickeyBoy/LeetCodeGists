### 面试题06. 从尾到头打印链表

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

示例 1：
```
输入：head = [1,3,2]
输出：[2,3,1]
```

### 解法 使用 reverse 函数
``` cpp
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> result;
        while(head) {
            result.push_back(head->val);
            head=head->next;
        }
        reverse(result.begin(),result.end());
        return result;
    }
};
```