### [494. 目标和](https://leetcode-cn.com/problems/target-sum/)

给你一个整数数组 nums 和一个整数 target 。

向数组中的每个整数前添加 '+' 或 '-' ，然后串联起所有整数，可以构造一个 表达式 ：

例如，nums = [2, 1] ，可以在 2 之前添加 '+' ，在 1 之前添加 '-' ，然后串联起来得到表达式 "+2-1" 。
返回可以通过上述方法构造的、运算结果等于 target 的不同 表达式 的数目。

### 解法：转化为 01背包 + 状态压缩

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        int N = nums.size();
        int sum = 0;
        for (int i=0;i<N;i++) { sum += nums[i]; }
        // 01背包
        int W = (sum-S)/2;
        if (sum-S < 0 || (sum-S) % 2 != 0) {
            return 0;
        }
        vector<int> dp = vector(W + 1, 0); // 前 x 个，目标和为 y，一共有几种表达式
        dp[0] = 1;
        for (int i = 1; i <= N; i++) {
            // 状态压缩
            for (int w = W; w >= 0; w--) { // 注意状态压缩后倒序
                if (w - nums[i-1] < 0) {
                    // 这种情况下只能选择不装入背包
                    // dp[w] = dp[w]; （省略）
                } else {
                    // 装入或者不装入背包，两种方法
                    dp[w] = dp[w - nums[i-1]] + dp[w];
                }
            }
        }
        return dp[W];
    }
};
```