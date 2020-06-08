### 714. 买卖股票的最佳时机含手续费

给定一个整数数组 prices，其中第 i 个元素代表了第 i 天的股票价格 ；非负整数 fee 代表了交易股票的手续费用。

你可以无限次地完成交易，但是你每笔交易都需要付手续费。如果你已经购买了一个股票，在卖出它之前你就不能再继续购买股票了。

返回获得利润的最大值。

注意：这里的一笔交易指买入持有并卖出股票的整个过程，每笔交易你只需要为支付一次手续费。

示例 1:
```
输入: prices = [1, 3, 2, 8, 4, 9], fee = 2
输出: 8
解释: 能够达到的最大利润:  
在此处买入 prices[0] = 1
在此处卖出 prices[3] = 8
在此处买入 prices[4] = 4
在此处卖出 prices[5] = 9
总利润: ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```
注意:
```
0 < prices.length <= 50000.
0 < prices[i] < 50000.
0 <= fee < 50000.
```


### 解法 1：状态机

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        if (n<=0) return 0;
        vector<int> hold = vector(n+1, 0); // 位于i天处于持有状态的财产
        vector<int> sold = vector(n+1, 0); // 位于i天处于持有未状态的财产
        hold[0] = -prices[0]; // base case
        for (int i=1;i<=n;i++) {
            hold[i] = max(hold[i-1], sold[i-1] - prices[i-1]); // 持有 = max(继续持有，新买入)
            sold[i] = max(sold[i-1], hold[i-1] + prices[i-1] - fee); // 未持有 = max(继续不持有，新卖出-fee)
        }
        return sold[n];
    }
};
```

### 解法 2：状态机 + 状态压缩

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        if (n<=0) return 0;
        // 状态压缩
        int hold = -prices[0]; // 位于i天处于持有状态的财产
        int sold = 0; // 位于i天处于持有未状态的财产
        for (int i=1;i<=n;i++) {
            int newHold = max(hold, sold - prices[i-1]); // 持有 = max(继续持有，新买入)
            int newSold = max(sold, hold + prices[i-1] - fee); // 未持有 = max(继续不持有，新卖出-fee)
            hold = newHold;
            sold = newSold;
        }
        return sold;
    }
};
```
