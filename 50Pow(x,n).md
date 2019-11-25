#### 50. Pow(x, n)

实现 pow(x, n) ，即计算 x 的 n 次幂函数。

示例 1:
```
输入: 2.00000, 10
输出: 1024.00000
```
示例 2:
```
输入: 2.10000, 3
输出: 9.26100
```
示例 3:
```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```
说明:

- 100.0 < x < 100.0
- n 是 32 位有符号整数，其数值范围是 [$−2^{31}$, $2^{31}$ − 1] 。

### 解法：快速幂

注意 int 越界的问题：如果 n == $−2^{31}$，不能直接带入 -n

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if(n<0) {
            // 注意 int 越界的问题
            return myPow(1/x,-(n+1))*(1/x);
        }
        double cur = 1;
        double mul = x;
        int remain = n;
        while(remain>0) {
            int temp = remain % 2;
            remain/=2;
            if(temp>0) {
                cur*=mul*temp;
            }
            mul*=mul;
        }
        return cur;
    }
};
```
