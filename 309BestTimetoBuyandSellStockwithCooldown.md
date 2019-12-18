### 309. Best Time to Buy and Sell Stock with Cooldown

给定一个整数数组，其中第 i 个元素代表了第 i 天的股票价格 。​

设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。
示例:
```
输入: [1,2,3,0,2]
输出: 3 
解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]
```

### 解法：动态规划，状态方程

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // sold-卖出，rest-未持有，hold-持有
        int sold = 0, rest = 0, hold = INT_MIN;
        for(auto &p : prices) {
            int preSold = sold;
            sold = hold + p; // 此时卖出，盈利增加p
            hold = max(hold, rest - p); // 持有=继续持有or冷冻期后买入
            rest = max(rest, preSold); // 不持有=继续不持有or之前已经卖出
        }
        return max(sold, rest);
    }
};
```
