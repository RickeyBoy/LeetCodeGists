### [1046. 最后一块石头的重量](https://leetcode-cn.com/problems/last-stone-weight/)


有一堆石头，每块石头的重量都是正整数。

每一回合，从中选出两块 最重的 石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x <= y。那么粉碎的可能结果如下：

如果 x == y，那么两块石头都会被完全粉碎；
如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。
最后，最多只会剩下一块石头。返回此石头的重量。如果没有石头剩下，就返回 0。

提示：
```
1 <= stones.length <= 30
1 <= stones[i] <= 1000
```

### 解法：大顶堆

```cpp
class Solution {
public:
    int lastStoneWeight(vector<int>& stones) {
        priority_queue<int> q;
        for (int s : stones) {
            q.push(s);
        }
        while (q.size()>1) {
            int a = q.top();
            q.pop();
            int b = q.top();
            q.pop();
            if (a!=b) {
                q.push(a-b);
            }
        }
        return q.size() > 0 ? q.top() : 0;
    }
};
```
