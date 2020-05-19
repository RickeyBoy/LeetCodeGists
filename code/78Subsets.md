### 78. Subsets

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:
```
输入: nums = [1,2,3]
输出:
[
 [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### 解法：递推

第 n 个 subset = 第 n-1个 subset + 其中每个 vector 插入第 n 个数

```cpp
class Solution {
public:
    void addToSubsets(vector<vector<int>>& result, int x) {
        int size = result.size();
        for(int i=0;i<size;i++) {
            vector<int> temp = result[i];
            temp.push_back(x);
            result.push_back(temp);
        }
        return;
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result;
        result.push_back({});
        for(int i=0;i<nums.size();i++) {
            addToSubsets(result, nums[i]);
        }
        return result;
    }
};
```
