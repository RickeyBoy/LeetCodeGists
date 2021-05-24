### [664. 奇怪的打印机](https://leetcode-cn.com/problems/strange-printer/)

有台奇怪的打印机有以下两个特殊要求：

打印机每次只能打印由 同一个字符 组成的序列。
每次可以在任意起始和结束位置打印新字符，并且会覆盖掉原来已有的字符。
给你一个字符串 s ，你的任务是计算这个打印机打印它需要的最少打印次数。

 
示例 1：
```
输入：s = "aaabbb"
输出：2
解释：首先打印 "aaa" 然后打印 "bbb"。
```
示例 2：
```
输入：s = "aba"
输出：2
解释：首先打印 "aaa" 然后在第二个位置打印 "b" 覆盖掉原来的字符 'a'。
```

### 解法：动态规划

```cpp
class Solution {
public:
    vector<vector<int>> dp; // dp[i][j] = [i,j] 间最少打印次数
    int strangePrinter(string s) {
        int n = s.length();
        dp = vector(n, vector(n, 1));
        for (int l=1;l<n;l++) {
            for (int i=0;i<n-l;i++) {
                // 遍历计算 dp[i][i+l]
                if (s[i+l-1] == s[i+l]) {
                    dp[i][i+l] = dp[i][i+l-1];
                } else {
                    int minNeeds = dp[i][i+l-1] + 1; // 最多额外多用一次
                    for (int x=0;x<l-1;x++) {
                        // 从 i 开始，l 的长度拆成两瓣进行打印，新增的跟后半一起打印
                        if (s[i+x] == s[i+l]) minNeeds = min(minNeeds, dp[i][i+x] + dp[i+x+1][i+l-1]);
                    }
                    dp[i][i+l] = minNeeds;
                }
            }
        }
        return dp[0][n-1];
    }
};
```
