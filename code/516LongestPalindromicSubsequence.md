### 516. 最长回文子序列

给定一个字符串s，找到其中最长的回文子序列，并返回该序列的长度。可以假设s的最大长度为1000。

示例 1:
```
输入:
"bbbab"
输出:
4
一个可能的最长回文子序列为 "bbbb"。
```
示例 2:
```
输入:
"cbbd"
输出:
2
一个可能的最长回文子序列为 "bb"。
```

### 解法：类似 LCS 二维 dp

```cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        // dp[x][y] s[0..x] 和 s[j..n-1] 之间的最长回文串
        vector<vector<int>> dp = vector(n, vector(n+1,0));
        // 起点
        for (int i = 0; i < n; i++) dp[i][i] = 1;
        for (int i=n-1;i>=0;i--) {
            for (int j=i+1;j<n;j++) {
                if (s[i]==s[j]) {
                    // 相同字符串，回文长度+2
                    dp[i][j] = dp[i+1][j-1] + 2;
                } else {
                    // 必定有一个在最长回文串中
                    dp[i][j] = max(dp[i+1][j], dp[i][j-1]);
                }
            }
        }
        return dp[0][n-1];
    }
};
```
