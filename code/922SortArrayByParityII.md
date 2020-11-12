### [922. 按奇偶排序数组 II](https://leetcode-cn.com/problems/sort-array-by-parity-ii/)

给定一个非负整数数组 A， A 中一半整数是奇数，一半整数是偶数。

对数组进行排序，以便当 A[i] 为奇数时，i 也是奇数；当 A[i] 为偶数时， i 也是偶数。

你可以返回任何满足上述条件的数组作为答案。

 

示例：

输入：[4,2,5,7]
输出：[4,5,2,7]
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。
 

提示：
```
2 <= A.length <= 20000
A.length % 2 == 0
0 <= A[i] <= 1000
```


注意：
```
输入的字符串只包含小写字母
两个字符串的长度都在 [1, 10,000] 之间
```


### 解法：

```cpp
class Solution {
public:
    vector<int> sortArrayByParityII(vector<int>& A) {
        int odd = 1;
        int even = 0;
        int size = A.size();
        while (odd<size && even<size) {
            while(even<size && A[even]%2==0) even+=2;
            while(odd<size && A[odd]%2==1) odd+=2;
            if (odd<size && even<size) swap(A[odd], A[even]);
            odd+=2;
            even+=2;
        }
        return A;
    }
    void swap(int &a, int &b) {
        int temp = a;
        a = b;
        b = temp;
    }
};
```
