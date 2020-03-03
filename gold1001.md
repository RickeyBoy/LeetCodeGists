### 面试题 10.01. 合并排序的数组

给定两个排序后的数组 A 和 B，其中 A 的末端有足够的缓冲空间容纳 B。 编写一个方法，将 B 合并入 A 并排序。

初始化 A 和 B 的元素数量分别为 m 和 n。

示例:
```
输入:
A = [1,2,3,0,0,0], m = 3
B = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

### 解法：倒着排序

``` cpp
class Solution {
public:
    // 倒序排列
    void merge(vector<int>& A, int m, vector<int>& B, int n) {
        int a = m-1, b = n-1; // a b 代表 A B 该被比较的 index
        while(1) {
            if(a>=0&&b>=0) {
                // 比较，将大数放在数列 A 的最后一个没有排序好的位置
                if(A[a]<B[b]) {
                    A[a+b+1] = B[b];
                    b--;
                } else {
                    A[a+b+1] = A[a];
                    a--;
                }
            } else if (b>=0) {
                // A 已经用完了，将 B 迁移到 A 上
                A[b] = B[b];
                b--;
            } else if (a>=0) {
                // B 已经用完了，直接返回
                return;
            } else {
                return;
            }
        }
        return;
    }
};
```