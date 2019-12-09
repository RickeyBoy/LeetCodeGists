### 132. Palindrome Partitioning II

给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。

返回符合要求的最少分割次数。

示例:
```
输入: "aab"
输出: 1
解释: 进行一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。
```

### 解法：动态规划

```cpp
class Solution {
public:
    int minCut(string s) {
        // minStep[i] 前 i+1 个字符的最小 step
        vector<int> minStep(s.size(), INT_MAX);
        vector<vector<bool>> dp = vector(s.size(), vector(s.size(), false));
        for(int i=0;i<s.size();i++) {
            int minI = i;
            for(int j=0;j<=i;j++) {
                if(s.at(i) == s.at(j) && (j+1>i-1 || dp[j+1][i-1])) {
                    dp[j][i] = true;
                    if(j==0) minI = 0;
                    else minI = min(minI, minStep[j-1]+1);
                }
            }
            minStep[i]=minI;
        }
        return minStep.back();
    }
};
```
