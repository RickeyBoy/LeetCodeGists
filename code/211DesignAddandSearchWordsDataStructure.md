#### [211. 添加与搜索单词 - 数据结构设计](https://leetcode.cn/problems/design-add-and-search-words-data-structure/)

请你设计一个数据结构，支持 添加新单词 和 查找字符串是否与任何先前添加的字符串匹配 。

实现词典类 WordDictionary ：

WordDictionary() 初始化词典对象
void addWord(word) 将 word 添加到数据结构中，之后可以对它进行匹配
bool search(word) 如果数据结构中存在字符串与 word 匹配，则返回 true ；否则，返回  false 。word 中可能包含一些 '.' ，每个 . 都可以表示任何一个字母。


示例：
```
输入：
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
输出：
[null,null,null,null,false,true,true,true]

解释：
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // 返回 False
wordDictionary.search("bad"); // 返回 True
wordDictionary.search(".ad"); // 返回 True
wordDictionary.search("b.."); // 返回 True
```

提示：
```
1 <= word.length <= 25
addWord 中的 word 由小写英文字母组成
search 中的 word 由 '.' 或小写英文字母组成
最多调用 104 次 addWord 和 search
```

### 解法：二维数组 Trie 字典树 + DFS

```cpp
const int maxn = 25 * 1e4;
class WordDictionary {
private:
    int next[maxn][26]; // next[x][y] = c，表示结点 x 的 y 字符指向的下一个结点是 c
    bool exist[maxn];  // 该结点结尾的字符串是否存在
    int cnt; // 节点个数
public:
    WordDictionary() {
        memset(exist,false,sizeof exist);
        memset(next,0,sizeof next);
        cnt = 0;
    }
    
    void addWord(string word) {
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
        return dfs(word, 0, 0);
    }
    bool dfs(string word, int p, int i) {
        if (i==word.size()) {
            // 到结尾了
            return exist[p];
        }
        if (word[i] == '.') {
            for (int x = 0; x<= 25; x++) {
                // 尝试所有字母的匹配
                if (next[p][x] != 0 && dfs(word, next[p][x], i+1)) return true;
            }
            return false;
        } else {
            return next[p][word[i]-'a'] != 0 && dfs(word, next[p][word[i]-'a'], i+1);
        }
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */
```