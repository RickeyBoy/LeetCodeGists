### [127. Word Ladder](https://leetcode.cn/problems/word-ladder/)

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return *the **number of words** in the **shortest transformation sequence** from* `beginWord` *to* `endWord`*, or* `0` *if no such sequence exists.*

 

**Example 1:**

```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.
```

**Example 2:**

```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
```

 

**Constraints:**

- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
- `beginWord != endWord`
- All the words in `wordList` are **unique**.

### 解法：Queue + BFS

- BFS
- wordList 中删除对应的元素，来标记 visited

```cpp
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        queue<string> current;
        unordered_set wordSet(wordList.begin(), wordList.end());
        int n = beginWord.size();
        // edge case
        if (wordSet.count(endWord) == 0) {
            return 0;
        }
        // init
        int step = 1;
        current.push( beginWord );
        // start
        while (!current.empty()) {
            int size = current.size();
            printf("next round, size = %d\n", current.size());
            for (int x=0;x<size;x++) { // current size may change!!
                string str = current.front();
                current.pop();
                printf("str: %s, step = %d\n", str.c_str(), step);
                // find the solution
                if (str == endWord) {
                    return step;
                }
                // search
                for (int i=0;i<n;i++) {
                    string newWord = str;
                    for (char c='a';c<='z';c++) {
                        newWord[i]=c;
                        // valid word
                        if (wordSet.count(newWord)) {
                            current.push(newWord);
                            wordSet.erase(newWord); // visited
                        }
                    }
                }
            }
            step+=1;
        }
        return 0;
    }
};
```
