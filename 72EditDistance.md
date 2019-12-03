### 72. Edit Distance

给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

1. 插入一个字符
2. 删除一个字符
3. 替换一个字符


示例 1:
```
输入: word1 = "horse", word2 = "ros"
输出: 3
解释: 
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```
示例 2:
```
输入: word1 = "intention", word2 = "execution"
输出: 5
解释: 
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```


### 解法： 动态规划

定义：$d[i][j]$ =  word1 前 i 个字符的子串，与 word2 前 j 个字符的子串的编辑距离
递归过程： 
- 由 $d[i-1][j]$ 、$d[i][j-1]$ 插入一个字符 $min（dp[i-1][j]+1, dp[i][j-1]+1）$
- 先得到 $d[i-1][j-1]$ 的编辑距离，如果 word1[i] 与 word2[j] 相等，则直接得到（$d[i-1][j-1]$）；否则需要进行一步替换操作（$d[i-1][j-1]+1$）

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();
        vector<vector<int>> dp(m+1, vector<int> (n+1,0));
        for(int i=0;i<=m;i++) {
            for(int j=0;j<=n;j++) {
                if(i==0) dp[i][j]=j;
                else if(j==0) dp[i][j]=i;
                else {
                    if(word1.at(i-1)==word2.at(j-1)) {
                        dp[i][j] = min({dp[i-1][j]+1, dp[i][j-1]+1 , dp[i-1][j-1]});
                    } else {
                        dp[i][j] = min({dp[i-1][j]+1, dp[i][j-1]+1, dp[i-1][j-1]+1});
                    }
                }
            }
        }
        return dp[m][n];
    }
};
```


