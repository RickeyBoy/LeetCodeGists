#### [1252. 奇数值单元格的数目](https://leetcode.cn/problems/cells-with-odd-values-in-a-matrix/)

给你一个 m x n 的矩阵，最开始的时候，每个单元格中的值都是 0。

另有一个二维索引数组 indices，indices[i] = [ri, ci] 指向矩阵中的某个位置，其中 ri 和 ci 分别表示指定的行和列（从 0 开始编号）。

对 indices[i] 所指向的每个位置，应同时执行下述增量操作：

ri 行上的所有单元格，加 1 。
ci 列上的所有单元格，加 1 。
给你 m、n 和 indices 。请你在执行完所有 indices 指定的增量操作后，返回矩阵中 奇数值单元格 的数目。

### 解法：数学角度

```cpp
class Solution {
public:
    int oddCells(int m, int n, vector<vector<int>>& indices) {
        unordered_set<int> cols; // 最终需要 +1 的列数
        unordered_set<int> rows; // 最终需要 +1 的行数
        for (vector<int> v : indices) {
            if (rows.count(v[0])) {
                // 重复 +1 则抵消掉
                rows.erase(v[0]);
            } else {
                rows.insert(v[0]);
            }
            if (cols.count(v[1])) {
                // 重复 +1 则抵消掉
                cols.erase(v[1]);
            } else {
                cols.insert(v[1]);
            }
        }
        // 交点为偶数值，扣除交点个数*2（交点被重复算了两次）
        return m * cols.size() + n * rows.size() - 2 * cols.size() * rows.size();
    }
};
```
