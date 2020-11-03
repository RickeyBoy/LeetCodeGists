### 941. 有效的山脉数组

给定一个整数数组 A，如果它是有效的山脉数组就返回 true，否则返回 false。

让我们回顾一下，如果 A 满足下述条件，那么它是一个山脉数组：

A.length >= 3
在 0 < i < A.length - 1 条件下，存在 i 使得：
A[0] < A[1] < ... A[i-1] < A[i]
A[i] > A[i+1] > ... > A[A.length - 1]

示例 1：
```
输入：[2,1]
输出：false
```
示例 2：
```
输入：[3,5,5]
输出：false
```
示例 3：
```
输入：[0,3,2,1]
输出：true
```

### 解法：

```cpp
class Solution {
public:
    bool validMountainArray(vector<int>& A) {
        if (A.size() < 3) return false;
        bool isIncreasing = true;
        for (int i=1;i<A.size();i++) {
            if (isIncreasing) {
                if (A[i] > A[i-1]) continue; // strictly increasing
                else if (A[i] < A[i-1] && i > 1) isIncreasing = false; // peak (can't locate at A[0])
                else return false;
            } else {
                if (A[i] < A[i-1]) continue; // strictly decreasing
                else return false;
            }
        }
        if (isIncreasing) return false; // no peak
        return true;
    }
};
```
