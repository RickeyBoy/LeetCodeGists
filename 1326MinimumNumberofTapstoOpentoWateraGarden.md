### 1326. Minimum Number of Taps to Open to Water a Garden

在 x 轴上有一个一维的花园。花园长度为 n，从点 0 开始，到点 n 结束。

花园里总共有 n + 1 个水龙头，分别位于 [0, 1, ..., n] 。

给你一个整数 n 和一个长度为 n + 1 的整数数组 ranges ，其中 ranges[i] （下标从 0 开始）表示：如果打开点 i 处的水龙头，可以灌溉的区域为 [i -  ranges[i], i + ranges[i]] 。

请你返回可以灌溉整个花园的 最少水龙头数目 。如果花园始终存在无法灌溉到的地方，请你返回 -1 。

 

示例 1：
```
输入：n = 5, ranges = [3,4,1,1,0,0]
输出：1
解释：
点 0 处的水龙头可以灌溉区间 [-3,3]
点 1 处的水龙头可以灌溉区间 [-3,5]
点 2 处的水龙头可以灌溉区间 [1,3]
点 3 处的水龙头可以灌溉区间 [2,4]
点 4 处的水龙头可以灌溉区间 [4,4]
点 5 处的水龙头可以灌溉区间 [5,5]
只需要打开点 1 处的水龙头即可灌溉整个花园 [0,5] 。
```
示例 2：
```
输入：n = 3, ranges = [0,0,0,0]
输出：-1
解释：即使打开所有水龙头，你也无法灌溉整个花园。
```
示例 3：
```
输入：n = 7, ranges = [1,2,1,0,2,1,0,1]
输出：3
```
示例 4：
```
输入：n = 8, ranges = [4,0,0,0,0,0,0,0,4]
输出：2
```
示例 5：
```
输入：n = 8, ranges = [4,0,0,0,4,0,0,0,4]
输出：1
```

提示：
```
1 <= n <= 10^4
ranges.length == n + 1
0 <= ranges[i] <= 100
```

### 解法：预处理 + 贪心

```cpp
class Solution {
public:
    int minTaps(int n, vector<int>& ranges) {
        vector<pair<int,int>> covers;
        pair<int,int> aim;
        aim = make_pair(0,n);
        int curMaxRight = 0;
        for(int i=0;i<ranges.size();i++) {
            // 预处理，过滤被包含的无用区间
            if(i+ranges[i]>curMaxRight) {
                curMaxRight = i+ranges[i];
                covers.push_back(make_pair(i-ranges[i],i+ranges[i]));
            }
        }
        int steps = 0;
        while(covers.size()>0) {
            // 贪心，从两头开始压缩 aim 区间
            int step = tryToCover(aim, covers);
            if (step==1 || step==0) return steps+step;
            else if (step==-1) return -1;
            else steps+=step;
        }
        // 没有水龙头了，但是没有退出，说明无法覆盖
        return -1;
    }

    // 单次缩小区间所需要的步数，有 -1，0，1，2 四种情况
    int tryToCover(pair<int,int>& aim, vector<pair<int,int>>& covers) {
        if (aim.first>=aim.second) return 0; // 已经能覆盖了，直接返回
        // 缩小区间，记录单个 cover 能从左右能够缩小的最大范围
        int maxLeft = aim.first, minRight = aim.second;
        for(auto c : covers) {
            if(c.first<=aim.first && c.second>=aim.second) return 1; // 全覆盖
            else if (c.first<=aim.first && c.second<aim.second) {
                // 从左侧能覆盖到的最大部分
                maxLeft = max(c.second, maxLeft);
            } else if (c.first>aim.first && c.second>=aim.second) {
                // 从右侧能覆盖到的最大部分
                minRight = min(c.first, minRight);
            }
        }
        if(maxLeft == aim.first && minRight == aim.second) return -1; // aim 区间并没有缩小，说明无法覆盖
        // 去掉缩小区间后，无用的 cover
        vector<pair<int,int>> remains = {};
        for(auto c : covers) {
            if(c.first>=minRight || c.second<maxLeft) continue; // 对缩小区间无贡献
            remains.push_back(c);
        }
        // 更新 aim 和 covers
        aim = make_pair(maxLeft, minRight);
        covers = remains;
        return 2;
    }
};
```
