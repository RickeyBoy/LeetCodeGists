### [525. 连续数组](https://leetcode-cn.com/problems/contiguous-array/)

给定一个二进制数组 nums , 找到含有相同数量的 0 和 1 的最长连续子数组，并返回该子数组的长度。

 

示例 1:
```
输入: nums = [0,1]
输出: 2
说明: [0, 1] 是具有相同数量 0 和 1 的最长连续子数组。
```
示例 2:
```
输入: nums = [0,1,0]
输出: 2
说明: [0, 1] (或 [1, 0]) 是具有相同数量0和1的最长连续子数组。
```

提示：
```
1 <= nums.length <= 105
nums[i] 不是 0 就是 1
```


### 解法：前缀和 + map

```cpp
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp = vector(n+1, 0); // dp[i+1]: [0,i]区间内 1 比 0 多的个数
        unordered_map<int, int> map; // map[x]=y: dp=x 时候的最左侧 index
        int result = 0;
        // 初始化
        dp[0] = 0;
        map[0] = 0;
        for (int i=1;i<=n;i++) {
            dp[i] = dp[i-1] + (nums[i-1] == 1 ? 1 : -1);
            if (map.count(dp[i])) {
                result = max(result, i - map[dp[i]]);
            } else {
                map[dp[i]]=i;
            }
        }
        return result;
    }
};
```
