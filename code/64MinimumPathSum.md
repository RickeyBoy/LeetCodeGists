### 64. Minimum Path Sum

给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

示例:
```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```

### 解法：动态规划

可以利用 grid 节省空间（此题 int 不会越界，因为动态规划时是取 min 而不是和）

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        if(n==0) return 0;
        int m = grid[0].size();
        if(m==0) return 0;
        for(int i=0;i<n;i++) {
            for (int j=0;j<m;j++) {
                if (i==0&&j==0) {
                    continue;
                } else if (i==0) {
                    grid[i][j] += grid[i][j-1];
                } else if (j==0) {
                    grid[i][j] += grid[i-1][j];
                } else {
                    grid[i][j] += min(grid[i-1][j],grid[i][j-1]);
                }
            }
        }
        return grid[n-1][m-1];
    }
};
```

