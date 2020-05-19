### 84. Largest Rectangle in Histogram

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 



以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。

 



图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

 

示例:
```
输入: [2,1,5,6,2,3]
输出: 10
```

### 解法：单调栈

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> stack; //上升单调栈
        int result = 0;
        stack.push(-1); // 方便寻找 leftIndex
        heights.push_back(0); // 方便地保证每个元素都被弹出过
        for(int i=0;i<heights.size();i++) {
            while(stack.top()!=-1 && heights[stack.top()]>=heights[i]) {
                // 遇到了不符合单调增的新值
                // 每次弹出时，都以该点为基准计算最大面积
                int top = stack.top();
                stack.pop();
                int leftIndex = stack.top(); // 左侧更低的一个点，右侧更低的点是 i
                result = max(result, (i-leftIndex-1)*heights[top]);
            }
            stack.push(i);
        }
        return result;
    }
};
```
