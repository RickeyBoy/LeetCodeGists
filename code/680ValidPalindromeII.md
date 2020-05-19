### 680. 验证回文字符串 Ⅱ

给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。

示例 1:
```
输入: "aba"
输出: True
```
示例 2:
```
输入: "abca"
输出: True
解释: 你可以删除c字符。
```
注意:
```
字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。
```

### 解法：回文串判定分叉一次就行

```cpp
class Solution {
public:
    bool validPalindrome(string s) {
        if(s.size()<=2) return true;
        for(int i=0;i<s.size()/2;i++) {
            if(s.at(i)!=s.at(s.size()-1-i)) {
                return isValid(s,i+1,s.size()-1-i) || isValid(s,i,s.size()-1-i-1);
            }
        }
        return true;
    }
    bool isValid(string s, int left, int right) {
        while(right>left) {
            if(s.at(left)!=s.at(right)) return false;
            left++;
            right--;
        }
        return true;
    }
};
```
