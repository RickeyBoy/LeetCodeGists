### 322. Coin Change

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

示例 1:
```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
```
示例 2:
```
输入: coins = [2], amount = 3
输出: -1
```
说明:
你可以认为每种硬币的数量是无限的。


### 解法：动态规划

动态规划 steps[i]，代表所有硬币组合成总数为 i 的最少硬币个数。

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> steps = vector(amount+1,-1);
        steps[0]=0;
        for(int i=1;i<=amount;i++) {
            for(auto coin : coins) {
                if(i<coin || steps[i-coin]==-1) continue;
                else {
                    if(steps[i]==-1) steps[i]=steps[i-coin]+1;
                    else steps[i]=min(steps[i-coin]+1,steps[i]);
                }
            }
        }
        return steps[amount];
    }
};
```
