### 3. Longest Substring Without Repeating Characters

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
示例 2:
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
示例 3:
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

### 解法

滑动窗口

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> current;
        int left=0;
        int right=0;
        int res=0;
        while(right<s.size()) {
            if(current.find(s[right])==current.end()) {
                // 新字符不重复，滑动窗口拓展
                current.insert(s[right]);
                right++;
                res = max(res, right-left);
            } else {
                // 新字符重复，滑动窗口左侧收缩到无重复字符为止
                while(s[left]!=s[right]) {
                    current.erase(s[left]);
                    left++;
                }
                right++;
                left++;
            }
        }
        return res;
    }
};
```
