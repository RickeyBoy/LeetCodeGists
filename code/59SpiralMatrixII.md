### [59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

 

示例 1：
```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```


### 解法

```cpp
class Solution {
public:
    void nextStep(int &i, int &j, int n) {
        if (i<=j && j+i<n-1) {
            // 处于上半三角区域，下一步向右
            printf("(%d, %d) right\n", i, j);
            j++;
        } else if (i+j<=n-1 && i>j) {
            // 处于左半三角
            if (i==j+1) {
                // 刚好该转弯了
                printf("(%d, %d) right\n", i, j);
                j++;
            } else {
                // 下一步向上
                printf("(%d, %d) up\n", i, j);
                i--;
            }
        } else if (i+j>=n-1 && i<j) {
            // 处于右半三角，下一步向下
            printf("(%d, %d) down\n", i, j);
            i++;
        } else {
            // 处于下半三角，下一步向左
            printf("(%d, %d) left\n", i, j);
            j--;
        }
    }
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> result = vector(n, vector(n,0));
        int i=0, j=0;
        for (int x=1;x<=n*n;x++) {
            result[i][j] = x;
            nextStep(i,j,n);
        }
        return result;
    }
};
```

