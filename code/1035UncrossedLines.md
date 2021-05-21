### [1035. 不相交的线](https://leetcode-cn.com/problems/uncrossed-lines/)

在两条独立的水平线上按给定的顺序写下 nums1 和 nums2 中的整数。

现在，可以绘制一些连接两个数字 nums1[i] 和 nums2[j] 的直线，这些直线需要同时满足满足：

 nums1[i] == nums2[j]
且绘制的直线不与任何其他连线（非水平线）相交。
请注意，连线即使在端点也不能相交：每个数字只能属于一条连线。

以这种方法绘制线条，并返回可以绘制的最大连线数。

 

示例 1：
```
输入：nums1 = [1,4,2], nums2 = [1,2,4]
输出：2
解释：可以画出两条不交叉的线，如上图所示。 
但无法画出第三条不相交的直线，因为从 nums1[1]=4 到 nums2[2]=4 的直线将与从 nums1[2]=2 到 nums2[1]=2 的直线相交。
```


### 解法：LCS 算法，最长公共子序列

```cpp
class Solution {
public:
    int maxUncrossedLines(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();
        // dp[x][y] 代表 nums1[1..x] 和 nums2[1..y] 的 LCS 串
        vector<vector<int>> dp = vector(m+1, vector(n+1, 0));
        for (int i=1;i<=m;i++) {
            for (int j=1;j<=n;j++) {
                if (nums1[i-1]==nums2[j-1]) {
                    // 相同字符，在 LCS 串中
                    dp[i][j] = dp[i-1][j-1] + 1;
                } else {
                    // 不同字符，必定有一个不在 LCS 串中
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        return dp[m][n];  
    }
};
```