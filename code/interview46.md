### 面试题46. 把数字翻译成字符串

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

示例 1:
```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

提示：
```
0 <= num < 231
```

### 解法：一维 dp + 状态压缩

``` cpp
class Solution {
public:
    int translateNum(int num) {
        vector<int> nums = vector(0, 0);
        int x = num;
        while (x > 0) {
            nums.push_back(x%10);
            x = x / 10;
        }
        // dp[i] 前 i 位数字有多少种组合方式, 数据压缩
        int n = nums.size();
        int result = 1;
        int last = 1;
        // 从数字高位开始遍历
        for (int i=2;i<=n;i++) {
            int index = n - i;
            int last2Num = nums[index]+nums[index+1]*10; // 前两位数字的值
            if (last2Num <=25 && last2Num >= 10) {
                // 前两位有两种翻译方法
                int temp = result;
                result = result + last;
                last = temp;
            } else {
                last = result;
            }
        }
        return result;
    }
};
```