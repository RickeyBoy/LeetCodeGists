#### [48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/)

给定一个 n × n 的二维矩阵 matrix 表示一个图像。请你将图像顺时针旋转 90 度。

你必须在 原地 旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要 使用另一个矩阵来旋转图像。


### 解法：分点旋转

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int size = matrix.size();
        int mid = matrix.size()/2 - 1;
        for (int i=0; i<=mid; i++) {
            for (int j=0; j<=mid; j++) {
                rotatePoint(matrix,i,j,size);
            }
        }
        if (size%2==1) {
            for (int j=0;j<=mid;j++) {
                rotatePoint(matrix,mid+1,j,size);
            }
        }
    }
    // 旋转相关联的四个点
    void rotatePoint(vector<vector<int>>& matrix, int i, int j, int size) {
        // 左上 右上 右下 左下
        // [0,1] [1,3] [3,2] [2,0], size = 4
        // [i,j] [j,size-i-1] [size-i-1, size-j-1] [size-j-1, i]
        int temp = matrix[i][j];
        matrix[i][j] = matrix[size-j-1][i]; // 左下 -> 左上
        matrix[size-j-1][i] = matrix[size-i-1][size-j-1]; // 右下 -> 左下
        matrix[size-i-1][size-j-1] = matrix[j][size-i-1]; // 右上 -> 右下
        matrix[j][size-i-1] = temp; // 左上 -> 右上
        printf("%d->%d  ", temp, matrix[size-j-1][i]);
    }
};
```
