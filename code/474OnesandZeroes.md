### 474. 一和零

在计算机界中，我们总是追求用有限的资源获取最大的收益。

现在，假设你分别支配着 m 个 0 和 n 个 1。另外，还有一个仅包含 0 和 1 字符串的数组。

你的任务是使用给定的 m 个 0 和 n 个 1 ，找到能拼出存在于数组中的字符串的最大数量。每个 0 和 1 至多被使用一次。

注意:
```
给定 0 和 1 的数量都不会超过 100。
给定字符串数组的长度不会超过 600。
```
示例 1:
```
输入: Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3
输出: 4

解释: 总共 4 个字符串可以通过 5 个 0 和 3 个 1 拼出，即 "10","0001","1","0" 。
```
示例 2:
```
输入: Array = {"10", "0", "1"}, m = 1, n = 1
输出: 2

解释: 你可以拼出 "10"，但之后就没有剩余数字了。更好的选择是拼出 "0" 和 "1" 。
```

### 解法1：01背包+状态压缩

```cpp
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        int size = strs.size();
        // dp[x][y][z] 前 x 个字符串，y 个 0，z 个 1 的条件下的结果
        // 递推关系只依赖 i-1，所以可以压缩
        vector<vector<int>> dp = vector(m+1, vector(n+1, 0));
        for (int i=0;i<size;i++) {
            int c1 = count1(strs[i]);
            int c0 = strs[i].size()-c1;
            // 压缩后需要倒序遍历
            for (int j=m;j>=0;j--) {
                for (int k=n;k>=0;k--) {
                    if (c0<=j && c1<=k) {
                        // 可选拼 or 不拼当前的字符串
                        dp[j][k] = max(dp[j][k], dp[j-c0][k-c1] + 1);
                    }
                }
            }
        }
        return dp[m][n];
    }
    // 字符串中 1 的个数
    int count1(string s) {
        int count = 0;
        for (auto c : s) {
            if (c=='1') count++;
        }
        return count;
    }
};
```