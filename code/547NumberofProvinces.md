### [547. 省份数量](https://leetcode-cn.com/problems/number-of-provinces/)

有 n 个城市，其中一些彼此相连，另一些没有相连。如果城市 a 与城市 b 直接相连，且城市 b 与城市 c 直接相连，那么城市 a 与城市 c 间接相连。

省份 是一组直接或间接相连的城市，组内不含其他没有相连的城市。

给你一个 n x n 的矩阵 isConnected ，其中 isConnected[i][j] = 1 表示第 i 个城市和第 j 个城市直接相连，而 isConnected[i][j] = 0 表示二者不直接相连。

返回矩阵中 省份 的数量。

### 解法：并查集

```cpp
class Solution {
public:
    vector<int> parents;
    vector<int> size;
    void UnionFind(int totalNum) {
        parents = vector(totalNum,0);
        size = vector(totalNum,1);
        for(int i=0;i<totalNum;i++) {
            parents[i]=i;
        }
    }
    int find(int x) {
        if (x!=parents[x]) parents[x]=find(parents[x]); //顺手路径压缩
        return parents[x];
    }
    int unionSet(int x, int y) {
        int xx = find(x);
        int yy = find(y);
        if (xx==yy) return 0; // 没有新的合并
        if (size[xx] > size[yy]) swap(xx, yy); //启发式合并
        parents[xx] = yy;
        size[yy] += size[xx];
        return 1;
    }

    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        int result = n;
        UnionFind(n);
        for (int i=0;i<n;i++) {
            for (int j=0;j<i;j++) {
                if (isConnected[i][j]) {
                    result -= unionSet(i,j);
                }
            }
        }
        return result;
    }
};
```
