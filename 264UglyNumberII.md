### 264. Ugly Number II.md

编写一个程序，找出第 n 个丑数。

丑数就是只包含质因数 2, 3, 5 的正整数。

示例:
```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```
说明:  

* 1 是丑数。
* n 不超过1690。


### 解法：动态规划，3 个游标简化

```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> nums = {1};
        // i2: 乘以 2 之后得到的最小丑数
        int i2=0,i3=0,i5=0,cur=1;
        while(cur<n){
            // tmp = 新一个最小的丑数，每个丑数注定是乘以 2/3/5 得到的
            int tmp = min(2*nums[i2],min(3*nums[i3],5*nums[i5]));
            nums.push_back(tmp);
            if(tmp==2*nums[i2]) i2++;
            if(tmp==3*nums[i3]) i3++;
            if(tmp==5*nums[i5]) i5++;
            cur++;
        }
        return nums.back();
    }
};
```
