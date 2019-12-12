### 51. N-Queens

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。



上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

示例:
```
输入: 4
输出: [
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```

### 解法：回溯

用三个 set 来记录已经被占位的位置，这样做反而效率不够高。直接用 vector<Pair<int, int>> 来表示已有点的合集，每次新点通过 isValid 遍历检查整个 vector，貌似效率更高。

```cpp
class Solution {
public:
    vector<vector<string>> result;
    vector<string> create(int n, vector<int> raw) {
        vector<string> solution;
        for(int i=0;i<n;i++) {
            string str(n,'.');
            str.at(raw[i]) = 'Q';
            solution.push_back(str);
        }
        return solution;
    }
    void backtrace(int n, vector<int> &cur, set<int> &columns, set<int> &left, set<int> &right) {
        int row = cur.size();
        if(row==n) result.push_back(create(n, cur));
        for(int line=0;line<n;line++) {
            if(columns.count(line)>0 || left.count(row+line)>0 || right.count(row-line)>0) continue;
            else {
                // 合法位置
                cur.push_back(line);
                columns.insert(line);
                left.insert(row+line);
                right.insert(row-line); 
                backtrace(n, cur, columns, left, right);
                // 回溯
                cur.pop_back();
                columns.erase(line);
                left.erase(row+line);
                right.erase(row-line); 
            }
        }
    }
    vector<vector<string>> solveNQueens(int n) {
        vector<int> cur;
        set<int> col, left, right;
        backtrace(n,cur,col,left,right);
        return result;
    }
};
```