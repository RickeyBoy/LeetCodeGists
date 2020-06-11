### 739. 每日温度

根据每日 气温 列表，请重新生成一个列表，对应位置的输出是需要再等待多久温度才会升高超过该日的天数。如果之后都不会升高，请在该位置用 0 来代替。

例如，给定一个列表 temperatures = [73, 74, 75, 71, 69, 72, 76, 73]，你的输出应该是 [1, 1, 4, 2, 1, 1, 0, 0]。

提示：气温 列表长度的范围是 [1, 30000]。每个气温的值的均为华氏度，都是在 [30, 100] 范围内的整数。


### 解法：单调栈

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        stack<int> index; // 记录单调栈里数据对应的 index
        for(int i=0;i<T.size();i++) {
            while(!index.empty() && T[i]>T[index.top()]) {
                // 找到一个在 i 之前且温度比 T[i] 低的日子
                T[index.top()] = i-index.top();
                index.pop();
            }
            index.push(i);
        }
        // 没有更高温度的天气
        while(!index.empty()) {
            T[index.top()] = 0;
            index.pop();
        }
        return T;
    }
};
```
