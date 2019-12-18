### 188. Best Time to Buy and Sell Stock IV

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 k 笔交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:
```
输入: [2,4,1], k = 2
输出: 2
解释: 在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。
```
示例 2:
```
输入: [3,2,6,5,0,3], k = 2
输出: 7
解释: 在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```

### 解法1：动态规划，参考状态转移方程式

问题：内存爆了

```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        if(n<=1||k<1) return 0;
        vector<vector<int>> hold = vector(n+1,vector(k+1,0)); // 位于i天,交易j次时处于持有状态的财产
        vector<vector<int>> sold = vector(n+1,vector(k+1,0)); // 位于i天,交易j次处于持有未状态的财产
        hold[0] = vector(k+1,INT_MIN);
        for(int i=1;i<=n;i++) {
            for(int j=1;j<=k;j++) {
                // 第i天持有 = 从i-1天继续持有 or 从i天开始买入
                hold[i][j]=max(hold[i-1][j],sold[i-1][j-1]-prices[i-1]);
                // 第i天未持有 = 从i-1天继续未持有 or 在i天卖出
                sold[i][j]=max(sold[i-1][j],hold[i-1][j]+prices[i-1]);
            }
        }
        return sold[n][k];
    }
};
```

### 解法2：简化递推，只存 hold 和 sold 的昨天和今天

问题：仍然爆内存，k 过大的时候申请 k+1 的 vector 直接爆

```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        if(n<=1||k<1) return 0;
        vector<int> curHold = vector(k+1,INT_MIN); // 位于i天,交易j次时处于持有状态的财产
        vector<int> curSold = vector(k+1,0); // 位于i天,交易j次时处于持有状态的财产
        vector<int> preHold = vector(k+1,INT_MIN); // 记录前一天的 Hold 值
        vector<int> preSold = vector(k+1,0); // 记录前一天的 Sold 值
        for(int i=1;i<=n;i++) {
            for(int j=1;j<=k;j++) {
                // 第i天持有 = 从i-1天继续持有 or 从i天开始买入
                curHold[j]=max(preHold[j],preSold[j-1]-prices[i-1]);
                // 第i天未持有 = 从i-1天继续未持有 or 在i天卖出
                curSold[j]=max(preSold[j],preHold[j]+prices[i-1]);
                // 更新
                preHold=curHold;
                preSold=curSold;
            }
        }
        return curSold[k];
    }
};
```

### 解法3：改变遍历顺序，vector 方式从 k+1 到 n+1

通过了，但是效率很低，这种状态转移方程的方式需要维护很多中间状态，所以整体效率不高

```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        if(n<=1||k<1) return 0;
        // dp[0] 位于i天k次,交易j次时处于持有状态的财产
        // dp[1] 位于i天,交易j次时处于持有状态的财产
        vector<vector<int>> dp = {vector(n+1,INT_MIN), vector(n+1,0)};
        vector<int> preSold = vector(n+1,0); // 记录k-1次对应的 Sold 值
        int result=0,j=k;
        while(j>=1) {
            for(int i=1;i<=n;i++) {
                // 第i天持有 = 从i-1天继续持有 or 从i天开始买入
                dp[0][i]=max(dp[0][i-1],preSold[i-1]-prices[i-1]);
                // 第i天未持有 = 从i-1天继续未持有 or 在i天卖出
                dp[1][i]=max(dp[1][i-1],dp[0][i-1]+prices[i-1]);
            }
            if(dp[1][n]>result) {
                result = dp[1][n];
                preSold=dp[1];
            } else {
                // 如果结果不再增加，说明 k 再大也没有意义了，所以直接返回
                return result;
            }
            j--;
        }
        return result;
    }
};
```