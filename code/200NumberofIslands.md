### 200. Number of Islands

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

示例 1:
```
输入:
11110
11010
11000
00000
输出: 1
```
示例 2:
```
输入:
11000
11000
00100
00011
输出: 3
解释: 每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。
```


### 解法：并查集

```cpp
class UnionFind {
private:
    vector<int> parents;
    vector<int> size;
    
public:
    int count = 0;
    UnionFind(int totalNum) {
        parents = vector(totalNum,0);
        size = vector(totalNum,1);
        for(int i=0;i<totalNum;i++) {
            parents[i]=i;
        }
    }

    /* 
    由于路径压缩单次合并可能造成大量修改，有时路径压缩并不适合使用
    例如，在可持久化并查集、线段树分治 + 并查集中，一般使用只启发式合并的并查集
    */
    int find(int x) {
        if (x!=parents[x]) parents[x]=find(parents[x]); //顺手路径压缩
        return parents[x];
    }
    
    void unionSet(int x, int y) {
        int xx = find(x);
        int yy = find(y);
        if (xx==yy) return;
        if (size[xx] > size[yy]) swap(xx, yy); //启发式合并
        parents[xx] = yy;
        size[yy] += size[xx];
        count --;
    }
};
class Solution {
public:
    int x,y;
    int numIslands(vector<vector<char>>& grid) {
        x = grid.size(); if(x<=0) return 0;
        y = grid[0].size(); if(y<=0) return 0;
        UnionFind uf = UnionFind(x*y);
        for(int i=0;i<x;i++) {
            for(int j=0;j<y;j++) {
                if(grid[i][j]=='0') continue;
                uf.count ++;
                int curNode = node(i,j);
                // 每个点和左侧、上侧的点尝试连接
                if (i>0&&grid[i-1][j]=='1') uf.unionSet(node(i-1,j),curNode);
                if (j>0&&grid[i][j-1]=='1') uf.unionSet(node(i,j-1),curNode);
            }
        }
        // 得到最终结果
        return uf.count;
    }
    int node(int i, int j) {
        return i*y+j;
    }
};
```
