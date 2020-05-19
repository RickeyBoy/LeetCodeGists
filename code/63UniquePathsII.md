### 63. Unique Paths II

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

示例 1:
```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

### 解法：动态规划

可以利用 obstacleGrid 节省空间，但是 int 会越界。

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int n = obstacleGrid.size();
        if(n==0) return 0;
        int m = obstacleGrid[0].size();
        if(m==0) return 0;
        vector<vector<unsigned int>> vec(n , vector<unsigned int>(m, 0));
        for(int i=0;i<n;i++) {
            for (int j=0;j<m;j++) {
                if (obstacleGrid[i][j]==1) {
                    // obstacle
                    vec[i][j] = 0;
                } else {
                    // empty space
                    if (i==0&&j==0) {
                        vec[i][j] = 1;
                    } else if (i==0) {
                        vec[i][j] = vec[i][j-1];
                    } else if (j==0) {
                        vec[i][j] = vec[i-1][j];
                    } else {
                        vec[i][j] = vec[i-1][j] + vec[i][j-1];
                    }
                }
            }
        }
        return vec[n-1][m-1];
    }
};
```

