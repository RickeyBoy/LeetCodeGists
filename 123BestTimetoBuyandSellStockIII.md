### 123. Best Time to Buy and Sell Stock III

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:
```
输入: [3,3,5,0,0,3,1,4]
输出: 6
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```
示例 2:
```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```
示例 3:
```
输入: [7,6,4,3,1] 
输出: 0 
解释: 在这个情况下, 没有交易完成, 所以最大利润为 0。
```

### 解法：动态规划

根据题意，两次交易不能有重合。原题可以转化为：以 i 为切割点，左右两部分分别进行一笔交易赚的最大利润，即为这种情况下的最大利润。遍历所有可能 i 即可知道最终答案。

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        int result = 0;
        // right[i] 代表从 i 开始的 prices 序列，能赚的最大的钱
        vector<int> right = vector(n,0);
        int maxRight = 0;
        int resRight = 0;
        for(int i=n-1;i>=0;i--) {
            // 倒序遍历，动态规划得到 right 数组
            maxRight = max(prices[i], maxRight);
            right[i] = max(resRight, maxRight - prices[i]);
        }
        // 正序遍历，resLeft 代表截止到 i，prices 序列能赚的最大的钱
        int minLeft = INT_MAX;
        int resLeft = 0;
        for(int i=0;i<n;i++) {
            minLeft = min(prices[i], minLeft);
            resLeft = max(resLeft, prices[i] - minLeft);
            // resLeft + right[i] 代表以 i 为分割，两侧分别能赚到的钱的总和
            result = max(result, resLeft + right[i]);
        }
        return result;
    }
};
```
