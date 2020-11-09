### [973. 最接近原点的 K 个点](https://leetcode-cn.com/problems/k-closest-points-to-origin/)

我们有一个由平面上的点组成的列表 points。需要从中找出 K 个距离原点 (0, 0) 最近的点。

（这里，平面上两点之间的距离是欧几里德距离。）

你可以按任何顺序返回答案。除了点坐标的顺序之外，答案确保是唯一的。

 

示例 1：
```
输入：points = [[1,3],[-2,2]], K = 1
输出：[[-2,2]]
解释： 
(1, 3) 和原点之间的距离为 sqrt(10)，
(-2, 2) 和原点之间的距离为 sqrt(8)，
由于 sqrt(8) < sqrt(10)，(-2, 2) 离原点更近。
我们只需要距离原点最近的 K = 1 个点，所以答案就是 [[-2,2]]。
```

示例 2：
```
输入：points = [[3,3],[5,-1],[-2,4]], K = 2
输出：[[3,3],[-2,4]]
（答案 [[-2,4],[3,3]] 也会被接受。）
```
 

提示：
```
1 <= K <= points.length <= 10000
-10000 < points[i][0] < 10000
-10000 < points[i][1] < 10000
```

### 解法：Quick select 变体

```cpp
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int K) {
        int l = 0, r = points.size()-1;
        while(l <= r) {
            int index = partition(points,l,r);
            if(index==K) return vector(points.begin(),points.begin()+index);
            else if(index<K) l = index+1;
            else r = index-1;
        }
        return points;
    }

    void swap(vector<int> &a, vector<int> &b) {
        vector<int> temp = a;
        a = b;
        b = temp;
    }

    int dis(vector<int> p) {
        return p[0]*p[0] + p[1]*p[1];
    }

    int partition(vector<vector<int>>&vi, int low, int up) {
        vector<int> pivot = vi[up];
        int i = low-1;
        for (int j = low; j < up; j++) {
            if(dis(vi[j]) <= dis(pivot)) {
                i++;
                swap(vi[i], vi[j]);
            }
        }
        swap(vi[i+1], vi[up]);
        return i+1;
    }
};
```
