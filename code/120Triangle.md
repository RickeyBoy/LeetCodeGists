### 120. Triangle

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

例如，给定三角形：
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

说明：

如果你可以只使用 O(n) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。

### 解法：动态规划

1. 只用长度为 triangle.size() 的 dp 数组即可
2. 每次递推倒序遍历当前行，可以在 dp 自身上直接递推

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        if(n==0) return 0;
        if(n==1) return triangle[0][0];
        vector<int> dp(n,0);
        dp[0] = triangle[0][0];
        for(int i=1;i<n;i++) {
            for(int j=i;j>=0;j--) {
                if(j==0) dp[j]+=triangle[i][j];
                else if(j==i) dp[j] = dp[j-1]+triangle[i][j];
                else dp[j] = min(dp[j], dp[j-1])+triangle[i][j];
            }
        }
        int result=dp[0];
        for(int i=0;i<dp.size();i++) {
            result=min(dp[i],result);
        }
        return result;
    }
};
```
