### 20. Valid Parentheses

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:
```
输入: "()"
输出: true
```
示例 2:
```
输入: "()[]{}"
输出: true
```
示例 3:
```
输入: "(]"
输出: false
```
示例 4:
```
输入: "([)]"
输出: false
```
示例 5:
```
输入: "{[]}"
输出: true
```



### 解法

利用栈就行，注意不能 pop 空栈。

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack <char> stack;
        for(char& c : s) {
            if(c=='{' || c=='[' || c=='(') stack.push(c);
            else if(stack.empty()) return false;
            else if(c=='}') {
                if (stack.top()=='{') stack.pop();
                else return false;
            }
            else if(c==']') {
                if (stack.top()=='[') stack.pop();
                else return false;
            }
            else if(c==')') {
                if (stack.top()=='(') stack.pop();
                else return false;
            }
        }
        return stack.empty();
    }
};
```



### 复杂度分析

**时间复杂度**：$O(n)$
**空间复杂度**：$O(n)$


