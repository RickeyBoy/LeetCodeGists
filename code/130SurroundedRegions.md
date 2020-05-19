### 130. Surrounded Regions

给定一个二维的矩阵，包含 'X' 和 'O'（字母 O）。

找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。

示例:
```
X X X X
X O O X
X X O X
X O X X
```
运行你的函数后，矩阵变为：
```
X X X X
X X X X
X X X X
X O X X
```
解释:
```
被围绕的区间不会存在于边界上，换句话说，任何边界上的 'O' 都不会被填充为 'X'。 任何不在边界上，或不与边界上的 'O' 相连的 'O' 最终都会被填充为 'X'。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。
```

### 解法：并查集

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

class Solution {
public:
    int x, y;
    void solve(vector<vector<char>>& board) {
        x = board.size();
        if(x<=2) return;
        y = board[0].size();
        if(y<=2) return;

        int edgeNode = x*y;
        UnionFind uf = UnionFind(edgeNode+1);
        for (int i=0;i<x;i++) {
            for (int j=0;j<y;j++) {
                if (board[i][j]=='X') continue;
                int curNode = node(i,j);
                // 是否是边界点
                if (i==0||i==x-1||j==0||j==y-1) uf.unionSet(curNode,edgeNode);
                // 每个点和左侧、上侧的点尝试连接
                if (i>0&&board[i-1][j]=='O') uf.unionSet(node(i-1,j),curNode);
                if (j>0&&board[i][j-1]=='O') uf.unionSet(node(i,j-1),curNode);
            }
        }

        // 遍历得到最终图
        int findEdge = uf.find(edgeNode);
        for (int i=0;i<x;i++) {
            for (int j=0;j<y;j++) {
                if(board[i][j]=='O' && uf.find(node(i,j))!=findEdge) board[i][j]='X';
            }
        }
    }
    int node(int i, int j) {
        return i*y+j;
    }
};
```
