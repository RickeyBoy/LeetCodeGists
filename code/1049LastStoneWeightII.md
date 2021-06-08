#### [1049. 最后一块石头的重量 II](https://leetcode-cn.com/problems/last-stone-weight-ii/)


有一堆石头，用整数数组 stones 表示。其中 stones[i] 表示第 i 块石头的重量。

每一回合，从中选出任意两块石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x <= y。那么粉碎的可能结果如下：

如果 x == y，那么两块石头都会被完全粉碎；
如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。
最后，最多只会剩下一块 石头。返回此石头 最小的可能重量 。如果没有石头剩下，就返回 0。

### 解法：01背包+状态压缩

```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        int sum = accumulate(stones.begin(), stones.end(), 0);
        int N = stones.size(), m = sum / 2;
        // 01背包
        int W = sum/2;
        vector<bool> dp = vector(W + 1, false); // 前 x 个，目标和为 y，能否有组合方式
        dp[0] = true;
        for (int i = 1; i <= N; i++) {
            // 状态压缩
            for (int w = W; w >= 0; w--) { // 注意状态压缩后倒序
                if (w - stones[i-1] < 0) {
                    // 这种情况下只能选择不装入背包
                    // dp[w] = dp[w]; （省略）
                } else {
                    // 装入或者不装入背包，两种方法
                    dp[w] = dp[w - stones[i-1]] || dp[w];
                }
            }
        }
        // 寻找最小可能值
        for (int w=W;w>=0;w--) {
            if (dp[w]) return sum-2*w;
        }
        return 0;
    }
};
```
