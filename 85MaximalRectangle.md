### 85. Maximal Rectangle

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

示例:
```
输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6
```

### 解法：单调栈 + 动态规划

每行来预处理 + 对每行进行 84 题类似的解法

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> stack; //上升单调栈
        int result = 0;
        stack.push(-1); // 方便寻找 leftIndex
        heights.push_back(0); // 方便地保证每个元素都被弹出过
        for(int i=0;i<heights.size();i++) {
            while(stack.top()!=-1 && heights[stack.top()]>=heights[i]) {
                // 遇到了不符合单调增的新值
                // 每次弹出时，都以该点为基准计算最大面积
                int top = stack.top();
                stack.pop();
                int leftIndex = stack.top(); // 左侧更低的一个点，右侧更低的点是 i
                result = max(result, (i-leftIndex-1)*heights[top]);
            }
            stack.push(i);
        }
        heights.pop_back();
        return result;
    }
    int maximalRectangle(vector<vector<char>>& matrix) {
        if(matrix.size()==0) return 0;
        vector<int> row(matrix[0].size(), 0);
        int result = 0;
        for(int i=0;i<matrix.size();i++) {
            for(int j=0;j<matrix[0].size();j++) {
                if(matrix[i][j]=='0') row[j]=0;
                else row[j]+=1;
            }
            result = max(result, largestRectangleArea(row));
        }
        return result;
    }
};
```
