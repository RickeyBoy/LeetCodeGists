### 416. 分割等和子集

给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

注意:
```
每个数组中的元素不会超过 100
数组的大小不会超过 200
```

示例 1:
```
输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
```

示例 2:
```
输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.
```

### 解法：01 背包变种 + 状态压缩

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum%2!=0) return false;
        sum = sum/2; // 计算背包总重
        int N = nums.size();
        // dp[x][y] = 前 x 个是否能凑出总重 y
        // 进行了状态压缩，所以 dp[] 即可
        vector<bool> dp = vector(sum+1, false);
        dp[0] = true;
        for (int i=0;i<N;i++) {
            for (int w=sum;w>=0;w--) {
                if (w>=nums[i]) {
                    dp[w] = dp[w-nums[i]] || dp[w];  // 选 or 不选第 i-1 个 
                }
            }
        }
        return dp[sum];
    }
};
```