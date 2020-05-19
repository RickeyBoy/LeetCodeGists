### 32. Longest Valid Parentheses

给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

示例 1:
```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```
示例 2:
```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```

### 解法

左右循环扫描。
时间复杂度：$O(n)$
空间复杂度：$O(1)$

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        int result = 0;
        int left;
        int right;
        left = 0;
        right = 0;
        for(int i=0;i<s.size();i++) {
            if(s[i]=='(') left++;
            else right++;
            if(left==right) {
                result = max(result, left+right);
            } else if (right>left) {
                left=0;
                right=0;
            }
        }
        left = 0;
        right = 0;
        for(int i=s.size()-1;i>=0;i--) {
            if(s[i]==')') right++;
            else left++;
            if(left==right) {
                result = max(result, left+right);
            } else if (right<left) {
                left=0;
                right=0;
            }
        }
        return result;
    }
};
```
