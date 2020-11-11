### [514. 自由之路](https://leetcode-cn.com/problems/freedom-trail/)

电子游戏“辐射4”中，任务“通向自由”要求玩家到达名为“Freedom Trail Ring”的金属表盘，并使用表盘拼写特定关键词才能开门。

给定一个字符串 ring，表示刻在外环上的编码；给定另一个字符串 key，表示需要拼写的关键词。您需要算出能够拼写关键词中所有字符的最少步数。

最初，ring 的第一个字符与12:00方向对齐。您需要顺时针或逆时针旋转 ring 以使 key 的一个字符在 12:00 方向对齐，然后按下中心按钮，以此逐个拼写完 key 中的所有字符。

旋转 ring 拼出 key 字符 key[i] 的阶段中：

您可以将 ring 顺时针或逆时针旋转一个位置，计为1步。旋转的最终目的是将字符串 ring 的一个字符与 12:00 方向对齐，并且这个字符必须等于字符 key[i] 。
如果字符 key[i] 已经对齐到12:00方向，您需要按下中心按钮进行拼写，这也将算作 1 步。按完之后，您可以开始拼写 key 的下一个字符（下一阶段）, 直至完成所有拼写。

``` 
输入: ring = "godding", key = "gd"
输出: 4
解释:
 对于 key 的第一个字符 'g'，已经在正确的位置, 我们只需要1步来拼写这个字符。 
 对于 key 的第二个字符 'd'，我们需要逆时针旋转 ring "godding" 2步使它变成 "ddinggo"。
 当然, 我们还需要1步进行拼写。
 因此最终的输出是 4。
```

提示：
```
ring 和 key 的字符串长度取值范围均为 1 至 100；
两个字符串中都只有小写字符，并且均可能存在重复字符；
字符串 key 一定可以由字符串 ring 旋转拼出。
```


### 解法：动态规划

```cpp
class Solution {
public:
    int findRotateSteps(string ring, string key) {
        int rL = ring.size();
        int kL = key.size();
        int curIndex = 0;
        int result = 0;
        // (ptr, step) ：拼了前 curIndex 个字符，当指针位于 ring 的 ptr 位置时花费的步数
        vector<pair<int,int>> steps;
        vector<pair<int,int>> newSteps;
        steps.push_back(make_pair(0,0)); // 起始，ptr 位于 0，已花费 0 步
        while (curIndex<key.size()) {
            int curResult = INT_MAX; // 这一轮中的最小步数
            for (int i = 0;i<ring.size();i++) {
                if (ring[i] == key[curIndex]) {
                    // 可以将指针旋转到 ring 的第 i 位，记录此时需要的步数
                    int curS = minDistanceOf(steps, i, rL);
                    newSteps.push_back(make_pair(i,curS));
                    curResult = min(curResult, curS);
                }
            }
            // 拼完了这一轮，再来一轮
            steps = newSteps;
            newSteps.clear();
            curIndex++;
            result = curResult;
        }
        return result;
    }
    // 根据上一步的情况，计算下一步中的最短距离
    int minDistanceOf(vector<pair<int,int>> steps, int aimIndex, int totalL) {
        int minStep = INT_MAX;
        for (pair<int,int> step : steps) {
            // 因为可以顺时针、逆时针旋转，所以：
            // 最短旋转距离 = 直接旋转 or 绕一圈旋转
            int minDistance = min(abs(aimIndex - step.first), abs(totalL - abs(aimIndex - step.first)));
            // 最小步数 = 已有步数 + 最短旋转距离 + 按下按钮的一步
            minStep = min(minStep, step.second + minDistance + 1);
        }
        return minStep;
    }
};
```
