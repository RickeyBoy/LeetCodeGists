#### [208. 实现 Trie (前缀树)](https://leetcode.cn/problems/implement-trie-prefix-tree/)

Trie（发音类似 "try"）或者说 前缀树 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。

请你实现 Trie 类：

Trie() 初始化前缀树对象。
void insert(String word) 向前缀树中插入字符串 word 。
boolean search(String word) 如果字符串 word 在前缀树中，返回 true（即，在检索之前已经插入）；否则，返回 false 。
boolean startsWith(String prefix) 如果之前已经插入的字符串 word 的前缀之一为 prefix ，返回 true ；否则，返回 false 。


示例：
```
输入
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
输出
[null, null, true, false, true, null, true]

解释
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // 返回 True
trie.search("app");     // 返回 False
trie.startsWith("app"); // 返回 True
trie.insert("app");
trie.search("app");     // 返回 True
```



### 解法：二维数组+字典树

```cpp
const int maxn = 1e5 + 50;
class Trie {
private:
    int next[maxn][26]; // next[x][y] = c，表示结点 x 的 y 字符指向的下一个结点是 c
    bool exist[maxn];  // 该结点结尾的字符串是否存在
    int cnt; // 节点个数
public:
    Trie() {
        memset(exist,false,sizeof exist);
        memset(next,0,sizeof next);
        cnt = 0;
    }
    
    void insert(string word) {
        int p = 0; // 当前遍历到的节点
        for(auto x : word){
            int c = x - 'a';
            if (next[p][c] == 0) {
                next[p][c] = ++cnt; // 新增节点
            }
            p = next[p][c];
        }
        exist[p] = true; // 标记结束位
    }
    
    bool search(string word) {
        int p = 0; // 当前遍历到的节点
        for (int i=0; i<word.size(); i++) {
            p = next[p][word[i]-'a'];
            if (p <= 0) return false; // 没找到
        }
        if (exist[p] == false) return false; // 不是结尾
        return true;
    }
    
    bool startsWith(string prefix) {
        int p = 0; // 当前遍历到的节点
        for (int i=0; i<prefix.size(); i++) {
            p = next[p][prefix[i]-'a'];
            if (p <= 0) return false; // 没找到
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```
