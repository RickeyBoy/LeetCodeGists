### 53. Maximum Subarray

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:
```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```
进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

### 解法

动态规划。分治法反而不是最优解

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int curSum = 0; // 当前序列和
        int res = nums[0];
        for(auto const& value: nums) {
            if(curSum>0) {
                curSum += value;
            } else {
                curSum = value;
            }
            res = max(curSum, res);
        }
        return res;
    }
};
```

### 优化

KMP 算法
