### 69. Sqrt(x)

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:
```
输入: 4
输出: 2
```
示例 2:
```
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
 ```

### 解法

注意边界条件和乘法溢出的问题。

```cpp
class Solution {
public:
    int mySqrt(int x) {
        // 注意边界情况过滤
        if(x==0) return 0;
        else if(x<4) return 1;
        else if(x<9) return 2;
        int Min = 1;
        int Max = x/2;
        while(Max>Min+1) {
            int mid = Min + (Max-Min)/2;
            // 注意乘法可能溢出
            if(x/mid<=mid-1) {
                Max = mid;
            } else {
                Min = mid;
            }
        }
        return Min;
    }
};
```
