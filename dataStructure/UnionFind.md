# 并查集

数据结构讲解：[并查集 - OI Wiki](https://oi-wiki.org/ds/dsu/)

### 核心方法

- 查找（Find）：确定某个元素处于哪个子集；
- 合并（Union）：将两个子集合并成一个集合。

*注意！不支持集合的分离、删除。

### 优化方式

- 查找（Find）：路径压缩
- 合并（Union）：启发式合并

### 复杂度

- 时间复杂度：同时使用路径压缩和启发式合并之后，并查集的每个操作平均时间仅为 $$O(\alpha (n))$$ ，其中  $$\alpha$$ 为**阿克曼函数**的反函数，其增长极其缓慢，也就是说其单次操作的平均运行时间可以认为是一个很小的常数
- 空间复杂度： $$O(n)$$

### 例题

- [130. Surrounded Regions 被围绕的区域](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/130SurroundedRegions.md) - medium
- [200. Number of Islands 岛屿数量](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/200NumberofIslands.md) - medium

### 代码模板

##### UnionFind 并查集

```cpp
class UnionFind {
private:
    vector<int> parents;
    vector<int> size;
public:
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

    /* 非路径压缩
    int find(int node) {
        while(parents[node]!=node) {
            node = parents[node];
        }
        return node;
    }
    */
    
    void unionSet(int x, int y) {
        int xx = find(x);
        int yy = find(y);
        if (xx==yy) return;
        if (size[xx] > size[yy]) swap(xx, yy); //启发式合并
        parents[xx] = yy;
        size[yy] += size[xx];
    }
};
```

##### 200 number of islands 用并查集示例

```cpp
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
                // 每个点和左侧、上侧的点尝试连接
                if (i>0&&grid[i-1][j]=='1') uf.unionSet(node(i-1,j),node(i,j));
                if (j>0&&grid[i][j-1]=='1') uf.unionSet(node(i,j-1),node(i,j));
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

##### 加权并查集

```cpp
class Solution {
public:
    vector<int> parents; // 记录父节点
    vector<double> weight; // 节点到根节点的权重
    int find(int x) {
        if (x!=parents[x])  {
            int p = parents[x]; // 父节点
            int root = find(p); // 根节点
            weight[x] = weight[x] * weight[p]; // 更新权重
            parents[x] = root; // 顺带路径压缩
        }
        return parents[x];
    }
    void unionSet(int x, int y, double w) {
        int xx = find(x);
        int yy = find(y);
        parents[xx] = yy; // x 根节点指向 y 根节点
        weight[xx] = w * weight[y] / weight[x]; // 更新 xx 的 weight
    }
};
```

