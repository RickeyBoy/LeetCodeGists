### 54. Spiral Matrix

给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

示例 1:
```
输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
输出: [1,2,3,6,9,8,7,4,5]
```
示例 2:
```
输入:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
输出: [1,2,3,4,8,12,11,10,9,5,6,7]
```

### 解法

螺旋打印

```cpp
class Solution {
public:
    // 打印边框
    vector<int> borderOrder(vector<vector<int>>& matrix, int left, int right, int top, int bottom) {
        vector<int> res;
        // 打印上边框
        for(int j=left;j<=right;j++) {
            res.push_back(matrix[top][j]);
        }
        // 打印右边框
        for(int i=top+1;i<=bottom;i++) {
            res.push_back(matrix[i][right]);
        }
        if(bottom>top) {
            // 超过一行，打印下边框
            for(int j=right-1;j>=left;j--) {
                res.push_back(matrix[bottom][j]);
            }
        }
        if(right>left) {
            // 超过一列，打印左边框
            for(int i=bottom-1;i>=top+1;i--) {
                res.push_back(matrix[i][left]);
            }
        }
        return res;
    }
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> result;
        int left=0, right, top=0, bottom;
        if(matrix.size()==0) return result;
        right=matrix[0].size()-1;
        bottom=matrix.size()-1;
        // 依次螺旋打印边框
        while(left<=right && top<=bottom) {
            vector<int> temp = borderOrder(matrix, left, right, top, bottom);
            result.insert(result.end(), temp.begin(), temp.end());
            top++;right--;left++;bottom--;
        }
        return result;
    }
};
```

### 解法 2：

（Python）打印第一行，旋转余下的矩阵

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        while matrix:
            res += matrix.pop(0)
            matrix = list(map(list, zip(*matrix)))[::-1]
        return res
```

