### 42. Trapping Rain Water

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。



上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 感谢 Marcos 贡献此图。

示例:
```
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```

### 解法：单调栈

**核心点 1**：新增面积的递推公式

新增面积 = (h-自身高度) * 左右两个最近更高点的距离

**核心点 2**：利用单调栈快速找到最近两个更高点

单调递减栈的特点：可以快速找到最近的两个更高点

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        stack<int> s;// 单调递减栈
        int result = 0;
        for(int i=0;i<height.size();i++) {
            while(!s.empty()&&height[s.top()]<height[i]) {
                // 遇到增值，开始弹出
                int midH = height[s.top()]; // 被弹出的点的自身高度
                s.pop();
                if(!s.empty()) {
                    // h = 左侧第一个更高的点 & 右侧第一个更高的点的最小值
                    int h = min(height[s.top()], height[i]);
                    // 新增面积 = (h-自身高度) * 左右两个最近高点的距离
                    result += (i-s.top()-1)*(h-midH);
                }
            }
            s.push(i);
        }
        return result;
    }
};
```
