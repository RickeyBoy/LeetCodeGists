###9.Palindrome Number

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:
```
输入: 121
输出: true
```
示例 2:
```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```
示例 3:
```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

### 解法

`while(temp>reverseX)` 只需要翻转一半的数字即可判断是否是回文数。如果是奇数位，那么 `reverseX/10==temp`，如果是偶数位那么 `reverseX==temp`。

注意需要仔细，例外的情况：
- x<0，直接返回 false
- x 最后一位是 0 且大于 0 时，应为 false
- x == 0，应为 true

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if(x<0||(x%10==0&&x>0)) return false;
        int reverseX = 0;
        int temp = x;
        // 只需要翻转一半的数即可
        while(temp>reverseX) {
            reverseX = reverseX*10 + temp%10;
            temp = temp / 10;
        }
        return reverseX==temp||reverseX/10==temp;
    }
};
```

