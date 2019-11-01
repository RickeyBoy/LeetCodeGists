### 73. Set Matrix Zeroes

给定一个 m x n 的矩阵，如果一个元素为 0，则将其所在行和列的所有元素都设为 0。请使用原地算法。

示例 1:
```
输入: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
输出: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```
示例 2:
```
输入: 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出: 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```
进阶:

一个直接的解决方案是使用  O(mn) 的额外空间，但这并不是一个好的解决方案。
一个简单的改进方案是使用 O(m + n) 的额外空间，但这仍然不是最好的解决方案。
你能想出一个常数空间的解决方案吗？

### 解法

找到第一个 0，用其所在的行列来记录应该被设置为 0 的行列。

O(1) 空间复杂度。

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        if(matrix.size()==0) {
            // 处理边界条件
            return;
        }
        int zeroRow = -1;
        int zeroCol = -1;
        int rowCount = matrix.size();
        int colCount= matrix[0].size();
        
        for(int row=0;row<rowCount;row++) {
            for(int col=0;col<colCount;col++) {
                if(matrix[row][col]==0) {
                    if(zeroRow<0) {
                        // 找到第一个 0
                        zeroRow = row;
                        zeroCol = col;
                    } else {
                        // 后续的 0 记录在 [zeroRow][zeroCol] 行列中
                        matrix[zeroRow][col] = 0;
                        matrix[row][zeroCol] = 0;
                    }
                }
            }
        }
        // 无 0
        if(zeroRow<0&&zeroCol<0) return;
        // 根据 [zeroRow][zeroCol] 的记录填周围的 0；
        for(int row=0;row<rowCount;row++) {
            if(matrix[row][zeroCol]==0 && row!=zeroRow) {
                for(int col=0;col<colCount;col++) {
                    matrix[row][col] = 0;
                }
            }
        }
        for(int col=0;col<colCount;col++) {
            if(matrix[zeroRow][col]==0 && col!=zeroCol) {
                for(int row=0;row<rowCount;row++) {
                    matrix[row][col] = 0;
                }
            }
            
        }
        // 填 [zeroRow][zeroCol] 的 0；
        for(int row=0;row<rowCount;row++) {
            matrix[row][zeroCol] = 0;
        }
        for(int col=0;col<colCount;col++) {
            matrix[zeroRow][col] = 0;
        }
        return;
    }
};
```