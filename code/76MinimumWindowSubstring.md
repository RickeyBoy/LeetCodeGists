### 76. 最小覆盖子串

给你一个字符串 S、一个字符串 T，请在字符串 S 里面找出：包含 T 所有字母的最小子串。

示例：

输入: S = "ADOBECODEBANC", T = "ABC"
输出: "BANC"
说明：
```
如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。
```

### 解法：滑动窗口

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        unordered_map<char,int> needs,window;
        int sameCount = 0;
        int left = 0, right = 0;
        int minLeft = 0, minLength = INT_MAX;
        // 初始化
        for (auto c : t) needs[c]++;
        // 滑动窗口
        while (right < s.size()) {
            // 增大窗口
            if (needs.count(s[right])) {
                window[s[right]]++;
                if (window[s[right]] <= needs[s[right]]) {
                    sameCount++;
                }
            }
            right++;
            while (sameCount==t.size()) {
                // 记录最小串
                if(right-left<minLength) {
                    minLength = right-left;
                    minLeft = left;
                }
                // 缩小窗口
                if (needs.count(s[left])) {
                    window[s[left]]--;
                    if (window[s[left]] < needs[s[left]]) {
                        sameCount--;
                    }
                }
                left++;
            }
        }
        return minLength == INT_MAX ? "" : s.substr(minLeft, minLength);
    }
};
```
