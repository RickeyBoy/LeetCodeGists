#### [877. 石子游戏](https://leetcode-cn.com/problems/stone-game/)

亚历克斯和李用几堆石子在做游戏。偶数堆石子排成一行，每堆都有正整数颗石子 piles[i] 。

游戏以谁手中的石子最多来决出胜负。石子的总数是奇数，所以没有平局。

亚历克斯和李轮流进行，亚历克斯先开始。 每回合，玩家从行的开始或结束处取走整堆石头。 这种情况一直持续到没有更多的石子堆为止，此时手中石子最多的玩家获胜。

假设亚历克斯和李都发挥出最佳水平，当亚历克斯赢得比赛时返回 true ，当李赢得比赛时返回 false 。


### 解法：动态规划

```cpp
class Solution {
public:
    bool stoneGame(vector<int>& piles) {
        int n = piles.size();
        // dp(x,y) : [x,y]区间，先拿的人的获胜点数
        vector<vector<int>> dp = vector(n, vector(n,0));
        // 初始
        for (int i=0;i<n;i++) {
            dp[i][i]=piles[i];
        }
        // 递推所有区间
        for (int s=1;s<n;s++) { // s=区间长度
            for (int i=0;i<n-s;i++) { // i=区间起点
                dp[i][i+s] = max(
                    -dp[i+1][i+s]+piles[i], // 先拿 i
                    -dp[i][i+s-1]+piles[i+s] // 先拿 i+s
                    );
                // printf("dp(%d,%d) == %d\n", i, i+s, dp[i][i+s]);
            }
        }
        return dp[0][n-1] > 0;
    }
};
```
