### UnionFind 并查集

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

### 加权并查集

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

