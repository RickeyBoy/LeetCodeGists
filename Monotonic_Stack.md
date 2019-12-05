# 单调栈

顾名思义，单调栈即满足单调性的栈结构。与单调队列相比，其只在一端进行进出。

一篇非常好的讲解文章：[单调栈原理及应用 详解 附各种类型的题目练习](https://blog.csdn.net/zuzhiang/article/details/78134247)

两个相关的 LeetCode：

- [84. Largest Rectangle in Histogram 柱状图中最大的矩形](https://github.com/RickeyBoy/LeetCodeGists/blob/master/84LargestRectangleinHistogram.md) - hard
- [85. Maximal Rectangle 最大矩形](https://github.com/RickeyBoy/LeetCodeGists/blob/master/85MaximalRectangle.md) - hard

### 伪代码

```
insert x
while !sta.empty() && sta.top()<x
    sta.pop()
sta.push(x)
```

### 单调栈的核心意义

寻找数组元素和它右边第一个比它大的数的距离

时间复杂度 $O(n)$

### 单调栈：柱状图中的最大矩形

具体过程
1. 考虑第 i 个矩形
2. 找到其左右最近的，高度小于其本身的矩形，分别记为 leftIndex 和 rightIndex
3. 那么包含 i 的最大矩形面积：$(rightIndex-leftIndex)*height[i]$
4. 遍历所有 i，求得最大面积

核心：第二步，利用单调栈快速求得 leftIndex & rightIndex
对于单调栈特性而言，stack[j] 的 leftIndex = stack[j-1]，rightIndex = stack[j+1]

### 单调栈：最大矩形

如何将最大矩形的题目转换成单调栈的题目？

可以参考这篇文章: [POJ 3494 Largest Submatrix of All 1’s 单调栈应用 图解+代码详解](https://blog.csdn.net/zuzhiang/article/details/78136417)
