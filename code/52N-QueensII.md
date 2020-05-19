### 52. N-QueensII

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。



上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

给定一个整数 n，返回 n 皇后不同的解决方案的数量。

示例:
```
输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```

### 解法1：回溯

```cpp
class Solution {
public:
    int result;
    bool isValid(vector<int> columns, int line) {
        int row = columns.size();
        for(int i=0;i<row;i++) {
            if(columns[i]==line||(columns[i]+i)==(line+row)||(columns[i]-i)==(line-row)) return false;
        }
        return true;
    }
    void backtrace(int n, vector<int> &columns) {
        int row = columns.size();
        if(row==n) result++;
        for(int line=0;line<n;line++) {
            if(!isValid(columns, line)) continue;
            else {
                // 合法位置
                columns.push_back(line);
                backtrace(n, columns);
                // 回溯
                columns.pop_back();
            }
        }
    }
    int totalNQueens(int n) {
        vector<int> line;
        backtrace(n,line);
        return result;
    }
};
```