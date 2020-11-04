### 57. Insert Interval

给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

 

示例 1：
```
输入：intervals = [[1,3],[6,9]], newInterval = [2,5]
输出：[[1,5],[6,9]]
```
示例 2：
```
输入：intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出：[[1,2],[3,10],[12,16]]
解释：这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
```

### 解法

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> result;
        bool isInserted = false;
        for (vector<int> sub : intervals) {
            if (sub[1]<newInterval[0]) result.push_back(sub);
            else if (sub[0]>newInterval[1]) {
                if (!isInserted) { result.push_back(newInterval); isInserted = true; }
                result.push_back(sub);
            }
            else {
                newInterval[0] = min(newInterval[0],sub[0]);
                newInterval[1] = max(newInterval[1],sub[1]);
            }
        }
        if (!isInserted) result.push_back(newInterval);
        return result;
    }
};
```

