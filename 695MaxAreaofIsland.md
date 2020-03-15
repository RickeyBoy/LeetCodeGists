### 695. 岛屿的最大面积

给定一个包含了一些 0 和 1的非空二维数组 grid , 一个 岛屿 是由四个方向 (水平或垂直) 的 1 (代表土地) 构成的组合。你可以假设二维矩阵的四个边缘都被水包围着。

找到给定的二维数组中最大的岛屿面积。(如果没有岛屿，则返回面积为0。)

示例 1:
```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
对于上面这个给定矩阵应返回 6。注意答案不应该是11，因为岛屿只能包含水平或垂直的四个方向的‘1’。
```
示例 2:
```
[[0,0,0,0,0,0,0,0]]
对于上面这个给定的矩阵, 返回 0。
```

注意: 给定的矩阵grid 的长度和宽度都不超过 50。



### 解法：DFS

```cpp
class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        if(grid.size()<1||grid[0].size()<1) return 0;
        int res = 0;
        for (int i=0;i<grid.size();i++) {
            for (int j=0;j<grid[0].size();j++) {
                if (grid[i][j]==1) res = max( find(grid,i,j), res );
            }
        }
        return res;
    }
    // DFS
    int find(vector<vector<int>>& grid, int x, int y) {
        if (grid[x][y]==0) return 0;
        int size = 1;
        grid[x][y] = 0;
        if(x>0) size += find(grid,x-1,y);
        if(y>0) size += find(grid,x,y-1);
        if(x+1<grid.size()) size += find(grid,x+1,y);
        if(y+1<grid[0].size()) size += find(grid,x,y+1);
        return size;
    }
};
```
