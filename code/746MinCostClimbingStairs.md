### [746. 使用最小花费爬楼梯](https://leetcode-cn.com/problems/min-cost-climbing-stairs/)

数组的每个索引作为一个阶梯，第 i个阶梯对应着一个非负数的体力花费值 cost[i](索引从0开始)。

每当你爬上一个阶梯你都要花费对应的体力花费值，然后你可以选择继续爬一个阶梯或者爬两个阶梯。

您需要找到达到楼层顶部的最低花费。在开始时，你可以选择从索引为 0 或 1 的元素作为初始阶梯。


### 解法：DP

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        cost.push_back(0); // 新增，避免复杂判断
        for (int i = 2; i<cost.size(); i++) {
            cost[i] += min(cost[i-1],cost[i-2]);
        }
        return cost[cost.size()-1];
    }
};
```
