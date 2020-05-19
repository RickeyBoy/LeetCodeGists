### 5. Longest Palindromic Substring

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：
```
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```
示例 2：
```
输入: "cbbd"
输出: "bb"
```
### 解法 1

遍历 2n-1 个中心，以每个中心向左右找最长的回文串。
时间复杂度 $O(n^2)$，空间复杂度 $O(1)$。

```cpp
class Solution {
public:
    // 固定中心，找最长回文串
    int maxPalinedromeLen(string s, int left, int right) {
        int L = left, R = right;
        while(L>=0 && R<s.size() && s[L]==s[R]) {
            L--;R++;
        }
        return R-L-1;
    }
    string longestPalindrome(string s) {
        // 注意边界条件！
        if(s.length()<=1) return s;
        int curMax = 0;
        int maxLeft = 0;
        int left = 0, right = 0;
        // 遍历 2n-1 个中心
        while (right<s.size() && left<s.size()) {
            int tempMax = maxPalinedromeLen(s, left, right);
            if (tempMax>curMax) {
                curMax = tempMax;
                maxLeft = left;
            }
            if (right==left) right++;
            else left++;
        }
        return s.substr(maxLeft-(curMax-1)/2,curMax);
    }
};
```

### 解法 2 Manacher 算法
复杂度为  $O(n)$
