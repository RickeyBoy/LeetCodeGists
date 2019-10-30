### 70. Climbing Stairs

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：
```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```
示例 2：
```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```


### 解法 1： 动态规划

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if(n<=2) return n;
        vector<int> res(n);
        res[0]=1;
        res[1]=2;
        for(int i=2;i<n;i++) {
            res[i]=res[i-1]+res[i-2];
        }
        return res[n-1];
    }
};
```

### 解法 2：特征根法

递推关系式求通项公式：

递推关系式：$a_n = a_{n-1} + a_{n-2} (其中 n>=2, a_0 = 1, a_1 = 2)$

特征根公式：$x^2 = x + 1$

特征根：$\lambda_1=\frac{1+\sqrt{5}}{2}$、$\lambda_2=\frac{1-\sqrt{5}}{2}$

通项公式：$a_n = c_1 \times \lambda_1^n + c_2 \times \lambda_2^n$ 

带入$a_0$、$a_1$：得到 $c_1=\frac{1}{\sqrt{5}}(\frac{1+\sqrt{5}}{2})$、$c_2=-\frac{1}{\sqrt{5}}(\frac{1-\sqrt{5}}{2})$

最终可得通项公式。

