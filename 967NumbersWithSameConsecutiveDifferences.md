### 967. Numbers With Same Consecutive Differences

返回所有长度为 N 且满足其每两个连续位上的数字之间的差的绝对值为 K 的非负整数。

请注意，除了数字 0 本身之外，答案中的每个数字都不能有前导零。例如，01 因为有一个前导零，所以是无效的；但 0 是有效的。

你可以按任何顺序返回答案。

 

示例 1：
```
输入：N = 3, K = 7
输出：[181,292,707,818,929]
解释：注意，070 不是一个有效的数字，因为它有前导零。
```
示例 2：
```
输入：N = 2, K = 1
输出：[10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```

提示：
```
1 <= N <= 9
0 <= K <= 9
```


### 解法：动态规划

用 numsSameConsecDiff(int N-1, int K) 递推得到 numsSameConsecDiff(int N, int K)

```cpp
class Solution {
public:
    vector<int> results = {1,2,3,4,5,6,7,8,9};
    vector<int> numsSameConsecDiff(int N, int K) {
        if(N<1) return {};
        if(N==1) return {0,1,2,3,4,5,6,7,8,9};
        for(int i=1;i<N;i++) {
            vector<int> temp;
            for(auto item : results) {
                int last = item%10;
                if(K==0) {
                    temp.push_back(item*10+last);
                    continue;
                } else {
                    if(last+K<10) temp.push_back(item*10+last+K);
                    if(last-K>=0) temp.push_back(item*10+last-K);
                }
            }
            results = temp;
        }
        return results;
    }
};
```
