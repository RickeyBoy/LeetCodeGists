### [118. 杨辉三角](https://leetcode-cn.com/problems/pascals-triangle/)

给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

### 解法

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        if (numRows == 0) return {};
        vector<vector<int>> result;
        vector<int> cur = vector(1,1);
        result.push_back(cur);
        for (int i=1;i<numRows;i++) {
            cur = nextRow(cur);
            result.push_back(cur);
        }
        return result;
    }
    vector<int> nextRow(vector<int> row) {
        vector<int> next = {};
        next.push_back(1);
        for (int i=0;i<row.size()-1;i++) {
            next.push_back(row[i]+row[i+1]);
        }
        next.push_back(1);
        return next;
    }
};
```
