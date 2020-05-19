### 343. Integer Break

给定一个正整数 n，将其拆分为至少两个正整数的和，并使这些整数的乘积最大化。 返回你可以获得的最大乘积。

示例 1:
```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```
示例 2:
```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

### 解法

```cpp
class Solution {
public:
    int integerBreak(int n) {
        if(n == 2) return 1;
        if(n == 3) return 2;
        int a = 1;
        // 拆分成尽量多的 3
        int count = n/3;
        if(n%3==1) {
            return pow(3,count-1)*4;
        } else if (n%3==2) {
            return pow(3,count)*2;
        } else {
            return pow(3,count);
        }
    }
};
```
