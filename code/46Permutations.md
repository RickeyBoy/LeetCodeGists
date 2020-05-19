### 46. Permutations

给定一个没有重复数字的序列，返回其所有可能的全排列。

示例:
```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 解法：递推

k 个数的全排列 = k-1 个数的全排列的每个数组依次在各个位置插入第 k 个数

```cpp
class Solution {
public:
    vector<vector<int>> permuteI(vector<vector<int>> pre, vector<int>& nums, int i) {
        vector<vector<int>> res;
        int insert = nums[i];
        if(i==0) {
            res.push_back({insert});
        } else {
            for (int x=0;x<pre.size();x++) {
                for (int y=0;y<=i;y++) {
                    vector<int> preV = pre[x];
                    preV.insert(preV.begin()+y,insert);
                    res.push_back(preV);
                }
            }
        }
        return res;
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> result;
        if(nums.size()==0) return result;
        for (int i=0;i<nums.size();i++) {
            result = permuteI(result, nums, i);
        }
        return result;
    }
};
```
