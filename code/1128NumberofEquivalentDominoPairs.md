### [1128. 等价多米诺骨牌对的数量](https://leetcode-cn.com/problems/number-of-equivalent-domino-pairs/)

给你一个由一些多米诺骨牌组成的列表 dominoes。

如果其中某一张多米诺骨牌可以通过旋转 0 度或 180 度得到另一张多米诺骨牌，我们就认为这两张牌是等价的。

形式上，dominoes[i] = [a, b] 和 dominoes[j] = [c, d] 等价的前提是 a==c 且 b==d，或是 a==d 且 b==c。

在 0 <= i < j < dominoes.length 的前提下，找出满足 dominoes[i] 和 dominoes[j] 等价的骨牌对 (i, j) 的数量。

 

示例：
```
输入：dominoes = [[1,2],[2,1],[3,4],[5,6]]
输出：1
``` 

提示：
```
1 <= dominoes.length <= 40000
1 <= dominoes[i][j] <= 9
```

### 解法：模拟

```cpp
class Solution {
public:
    int numEquivDominoPairs(vector<vector<int>>& dominoes) {
        int result = 0;
        vector<int> vec = vector(100,0);
        for (vector<int> x : dominoes) {
            int k = x[1] > x[0] ? x[1]*10 + x[0] : x[0]*10 + x[1];
            result+=vec[k];
            vec[k]++;
        }
        return result;
    }
};
```
