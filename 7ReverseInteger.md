### 7.Reverse Integer

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例 1:
```
输入: 123
输出: 321 
```
示例 2:
```
输入: -123
输出: -321
```
示例 3:
```
输入: 120
输出: 21
```
注意:
假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [$−2^{31}$, $2^{31} − 1$]。请根据这个假设，如果反转后整数溢出那么就返回 0。

### 解法

倒序取 x 每一位的数字，再顺序给到 res。需要注意：

- 32bit 整数范围是  INT_MIN ~ INT_MAX
- 负数需要先变为正数在进行操作。由于 -INT_MIN 已经超过 int 范围了，所以需要先进性判断。

```cpp
class Solution {
public:
    int reverse(int x) {
      // 提前判断，避免 x==INT_MIN时，取 -x 时崩溃
        if(x>INT_MAX || x<-INT_MAX) return 0;
        long int res = 0;
        int temp = x;
        if(x<0) temp = -x;
        while(temp>0) {
            res = res*10 + temp%10;
            temp = temp/10;
        }
        if(x<0) res = -res;
        if(res>INT_MAX || res<INT_MIN) return 0;
        return res;
    }
};
```