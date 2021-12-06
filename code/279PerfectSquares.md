#### [279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

给你一个整数 n ，返回和为 n 的完全平方数的 最少数量 。

完全平方数 是一个整数，其值等于另一个整数的平方；换句话说，其值等于一个整数自乘的积。例如，1、4、9 和 16 都是完全平方数，而 3 和 11 不是。

 

示例 1：
```
输入：n = 12
输出：3 
解释：12 = 4 + 4 + 4
```
示例 2：
```
输入：n = 13
输出：2
解释：13 = 4 + 9
```
提示：
```
1 <= n <= 104
```

### 解法：利用 queue + pair 进行 BFS

```cpp
class Solution {
public:
    int numSquares(int n) {
        queue<pair<int, int>> q; // {当前剩余数，当前已使用的完全平方数次数}
        unordered_map<int,int> map; // f[x] = y，当前剩余数为 x 时的最小已使用次数为 y
        q.push({n, 0});
        map[n] = 0;
        // bfs：转化为二叉树层次遍历（类似）
        while(!q.empty()){
            auto head = q.front();
            int x = head.first;
            int cnt = head.second;
            q.pop();
            
            int m = static_cast<int>(sqrt(x));
            for(int i=1; i<= m; ++i){
                int temp = x - i*i;
                if (temp == 0) {
                    // 终止条件，剩余数为 0
                    return cnt+1;
                }
                if (map.count(temp) == 0) {
                    // 添加进下一层
                    q.push({temp, cnt+1});
                    // 并且记录
                    map[temp] = cnt + 1;
                }
            }
            
        }
        return 0;
    }
};
```
