### 415. 字符串相加

给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

注意：
```
num1 和num2 的长度都小于 5100.
num1 和num2 都只包含数字 0-9.
num1 和num2 都不包含任何前导零。
你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。
```

### 解法：01 背包变种 + 状态压缩

```cpp
class Solution {
public:
    string addStrings(string num1, string num2) {
        int l1 = num1.length();
        int l2 = num2.length();
        string result = "";
        int adder = 0;
        for (int i=0;i<max(l1,l2);i++) {
            int cur = value(num1,l1,i) + value(num2,l2,i) + adder;
            adder = cur / 10;
            result = to_string(cur%10) + result;
        }
        if (adder==1) result = "1" + result;
        return result;
    }
    int value(string s, int l, int x) {
        if (l-x-1<0) return 0;
        else {
            return s[l-x-1] - '0';
        }
    }
};
```