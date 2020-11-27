### [454. 四数相加 II](https://leetcode-cn.com/problems/4sum-ii/)

给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -228 到 228 - 1 之间，最终结果不会超过 231 - 1 。

例如:
```
输入:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

输出:
2
```

解释:
```
两个元组如下:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

### 解法：hash + 双循环

类似 two sum，可以想象 AB 双循环变成一个数组，CD 双循环变成一个数组，就是 two sum 了

```cpp
class Solution {
public:
    int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        unordered_map<int, int> map;
        int result = 0;
        for (int a : A) {
            for (int b : B) {
                if (map.count(a+b)) map[a+b]++;
                else map[a+b]=1;
            }
        }
        for (int c : C) {
            for (int d : D) {
                if (map.count(-c-d)) result += map[-c-d];
            }
        }
        return result;
    }
};
```