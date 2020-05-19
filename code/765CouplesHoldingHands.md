### 765. Couples Holding Hands

N 对情侣坐在连续排列的 2N 个座位上，想要牵到对方的手。 计算最少交换座位的次数，以便每对情侣可以并肩坐在一起。 一次交换可选择任意两人，让他们站起来交换座位。

人和座位用 0 到 2N-1 的整数表示，情侣们按顺序编号，第一对是 (0, 1)，第二对是 (2, 3)，以此类推，最后一对是 (2N-2, 2N-1)。

这些情侣的初始座位  row[i] 是由最初始坐在第 i 个座位上的人决定的。

示例 1:
```
输入: row = [0, 2, 1, 3]
输出: 1
解释: 我们只需要交换row[1]和row[2]的位置即可。
```
示例 2:
```
输入: row = [3, 2, 0, 1]
输出: 0
解释: 无需交换座位，所有的情侣都已经可以手牵手了。
```
说明:
```
len(row) 是偶数且数值在 [4, 60]范围内。
可以保证row 是序列 0...len(row)-1 的一个全排列。
```


### 解法：每次交换保证最左两个座位成为情侣

证明：[官方题解](https://leetcode-cn.com/problems/couples-holding-hands/solution/qing-lu-qian-shou-by-leetcode/)，通过连通分量不变进行证明

```cpp
class Solution {
public:
    int minSwapsCouples(vector<int>& row) {
        int result = 0;
        for(int i=0;i<row.size();i=i+2) {
            result += minSwapHelper(i,row);
        }
        return result;
    }
    // 交换位置，保证 index、index+1 是 couple
    int minSwapHelper(int index, vector<int>& row) {
        if (row[index]/2==row[index+1]/2) return 0;
        // 根据 index，寻找 couple，换到 index+1 的位置
        int couple = (row[index]%2==0) ? row[index]+1 : row[index]-1;
        for(int i=index+2;i<row.size();i++) {
            if (row[i]==couple) {
                swap(row[index+1], row[i]);
                return 1;
            }
        }
        return 0;
    }
};
```
