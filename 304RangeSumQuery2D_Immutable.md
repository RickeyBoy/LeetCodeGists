### 304. Range Sum Query 2D - Immutable

给定一个二维矩阵，计算其子矩形范围内元素的总和，该子矩阵的左上角为 (row1, col1) ，右下角为 (row2, col2)。


上图子矩阵左上角 (row1, col1) = (2, 1) ，右下角(row2, col2) = (4, 3)，该子矩形内元素的总和为 8。

示例:
```
给定 matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```
说明:

1. 你可以假设矩阵不可变。
2. 会多次调用 sumRegion 方法。
3. 你可以假设 row1 ≤ row2 且 col1 ≤ col2。



### 解法：动态规划

注意边界条件处理

```cpp
class NumMatrix {
public:
    // result[i][j] 代表原 matrix (0,0)~(i,j) 所有点之和
    vector<vector<int>> result;
    NumMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size();
        if(m==0) return;
        int n = matrix[0].size();
        for(int i=0;i<m;i++) {
            for(int j=0;j<n;j++) {
                // 在原矩阵上更新即可
                if(i==0&&j==0) continue;
                else if(i==0) matrix[i][j]+=matrix[i][j-1];
                else if(j==0) matrix[i][j]+=matrix[i-1][j];
                else {
                    matrix[i][j]=matrix[i][j]+matrix[i-1][j]+matrix[i][j-1]-matrix[i-1][j-1];
                }
            }
        }
        result = matrix;
        return;
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        if(row1==0&&col1==0) return result[row2][col2];
        else if(row1==0) return result[row2][col2]-result[row2][col1-1];
        else if(col1==0) return result[row2][col2]-result[row1-1][col2];
        else return result[row2][col2]-result[row2][col1-1]-result[row1-1][col2]+result[row1-1][col1-1];
    }
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```
