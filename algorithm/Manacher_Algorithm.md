# Manacher 算法



Manacher 算法可以在 $O(n)$ 时间复杂度内求出一个字符串的最长回文字串。

类似 KMP 算法：[KMP Algorithm - 字符串匹配](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/KMPAlgorithm.md)

基于中心扩散法：[5. Longest Palindromic Substring 最长回文子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/5LongestPalindromicSubstring.md)

一篇非常好的讲解文章：[Manacher 马拉车算法](https://blog.crimx.com/2017/07/06/manachers-algorithm/)



> 先在开头约定:
> 
> 原字符串 str
> 
> 原串 str 一样长的辅助数组 lens。lens[i] 表示以 str[i] 为中点的回串其中一边的长度
>
> iCenter 代表最右回文串的中心，iRight 代表其右端点。


### Manacher 本质：利用回文串的对称性进行动态规划

1. 预处理增加 # 分隔符，统一奇、偶长度的情况。
2. 维护辅助长度数组 lens，存储已知回文串的信息。
3. 维护最右回文串，特定情况下利用回文串的对称性，减少计算量。
4. 动态规划得到 plens数组的全部信息。


### 预处理：统一奇偶性

回文有奇偶长度两种情况，通过补充间隔符可以将这两种情况化简为奇数长度。
比如 `ABA` 补充为 `#A#B#A#` 中点还是 B，`ABBA` 补充为 `#A#B#B#A#` 中点为 #，最后可以去掉。

```cpp
// 得到预处理字符串
string str = "#";
for (int i = 0; i < s.size(); ++i) {
    str += s[i];
    str += "#";
}
```

### 辅助长度数组 lens

lens[i] 表示以 str[i] 为中点的回串其中一边的长度。最终最长回文串长度结果为 max(p[])。

lens[i] 的朴素计算法：中心扩散法。如果整个 lens 数组的计算全部采用中心扩散法，那么就与 [5. Longest Palindromic Substring 最长回文子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/5LongestPalindromicSubstring.md) 相同，时间复杂度为 $O(n^2)$

但是 lens[i] 也包含了以 i 为中心的回文串的信息，所以在递推过程中，可以利用这个信息减少计算量。部分后续节点有可能不需要进行朴素计算。


### 朴素计算方法

```cpp
int centerSpread(string s, int center) {
    // left = right 的时候，此时回文中心是一个空隙，回文串的长度是奇数
    // right = left + 1 的时候，此时回文中心是任意一个字符，回文串的长度是偶数
    int len = s.size();
    int i = center - 1;
    int j = center + 1;
    int step = 0;
    while (i >= 0 && j < len && s[i] == s[j]) {
        i--;
        j++;
        step++;
    }
    return step;
}
```

### 带起始长度的朴素计算方式

```cpp
int centerSpread(string s, int center, int initLen) {
        int result = initLen;
        // 精简代码
        while(center+result+1<s.size() && center-result-1 >= 0 && s[center+result+1]==s[center-result-1]) {
            result++;
        }
        return result;
    }
```


### 最右回文串 iCenter + iRight

我们维护一个已知最右的回串，设其中心点 iCenter 以及其最右点 iRight。显然两者有这么的关系:

```cpp
iRight = iCenter + lens[iCenter]。
```

### 最不理想的情况

如果 i 与最右回文串没有交集，即 `iRight <= i` 时，只能使用朴素计算，从长度 0 开始遍历。也就是 `centerSpread(str, i, 0)`。

### 理想情况

那么我们维护最右回文串的意义是什么？当 i 与回文串有交集的时候，可以利用回文镜像对称的特点，减少部分对 lens 的朴素计算。

比如 `OABAXABAO` 第二个 B 由于是以 X 为中心的回文串的右分支中的一部分，所以它的 lens 和第一个 B 的 lens 完全相等，也就是 lens[6] = lens[2]。

理想情况下，我们可以复制 `lens[2*iCenter-i]` 的值，但是这也有一定的条件：

理想情况条件：i 中心回文串长度 < 最右回文串右支长度，即 `lens[2*iCenter-i] < iRight - i` 

理想情况触发后：`lens[i]=lens[2*iCenter-i]`

### 两种边界情况：右贴界 + 左越界

右贴界：

对于 `OABAXABA...` 第二个 B 只能确定 lens[6] >= lens[2]，所以在这种情况下仍需采用朴素计算方式，不过可以进行一定的改良，让朴素计算方式的起始长度变成 lens[2]。

右贴界的条件：`i+lens[2*iCenter-i]==iRight`

右贴界触发之后：使用优化之后的朴素计算方式 centerSpread(string s, int center, int initLen)，其中`initLen=lens[2*iCenter-i]`

左越界：

对于 `XABAXABA...` 因为第一个 B 的回文串超过了中心点，所以第二个 B 直接复制 lens[2] 的话会超过当前最右回文串的范围，所以仍需采用朴素计算。不过起始长度可以变为最右回文串的范围内的最大长度：`iRight-i`。

左越界条件：`lens[2*iCenter-i]>iRight-i`

左越界触发之后：使用优化之后的朴素计算方式 centerSpread(string s, int center, int initLen)，其中`initLen=iRight-i`

### 理想情况与边界情况的整合

根据上面的情况，代码如下：

```cpp
// i 镜面对称点的坐标
int iMirror = 2*iCenter-i;
if (lens[iMirror] < iRight - i) {
    // 理想情况
    lens[i] = lens[iMirror];
} else if (lens[iMirror] == iRight - i) {
    // 右贴界
    lens[i] = centerSpread(str, i, lens[iMirror]);
} else { // lens[iMirror] > iRight - i
    // 左越界
    lens[i] = centerSpread(str, i, iRight - i);
}
```

上述代码还可以进一步整合，对于理想情况，我们也可以改写成下面的代码：

```cpp
// i 镜面对称点的坐标
int iMirror = 2*iCenter-i;
if (lens[iMirror] < iRight - i) {
    // 理想情况
    lens[i] = centerSpread(str, i, lens[iMirror]);
} else if (lens[iMirror] == iRight - i) {
    // 右贴界
    lens[i] = centerSpread(str, i, lens[iMirror]);
} else { // lens[iMirror] > iRight - i
    // 左越界
    lens[i] = centerSpread(str, i, iRight - i);
}
```

因为在理想情况下，可以直接得到 `lens[i] = lens[iMirror]`，在此基础之上我们在进行朴素计算 `centerSpread` 也会直接返回，不会进一步增加长度，所以两者代码是等价的。

那么我们再观察上述代码，可以进一步合并理想情况与右贴界的情况：

```cpp
// i 镜面对称点的坐标
int iMirror = 2*iCenter-i;
if (lens[iMirror] <= iRight - i) {
    // 理想情况 + 右贴界
    lens[i] = centerSpread(str, i, lens[iMirror]);
} else { // lens[iMirror] > iRight - i
    // 左越界
    lens[i] = centerSpread(str, i, iRight - i);
}
```

再精简过后就是

```cpp
// i 镜面对称点的坐标
int iMirror = 2*iCenter-i;
// 朴素计算的起始长度
int initLen = min(lens[iMirror], iRight - i);
// 综合了三种情况
lens[i] = centerSpread(str, i, initLen);
```

### 最终代码

```cpp
class Solution {
public:
    void replaceAll(std::string& str, const std::string& from, const std::string& to) {
        if(from.empty()) return;
        size_t start_pos = 0;
        while((start_pos = str.find(from, start_pos)) != std::string::npos) {
            str.replace(start_pos, from.length(), to);
            start_pos += to.length(); // In case 'to' contains 'from', like replacing 'x' with 'yx'
        }
    }
    int centerSpread(string s, int center, int initLen) {
        int result = initLen;
        // 精简代码
        while(center+result+1<s.size() && center-result-1 >= 0 && s[center+result+1]==s[center-result-1]) {
            result++;
        }
        return result;
    }
    string longestPalindrome(string s) {
        int maxCenter = 1;
        unordered_map<int,int> lens;
        int iCenter = 0;
        int iRight = 0;
        // 得到预处理字符串
        string str = "#";
        for (int i = 0; i < s.size(); ++i) {
            str += s[i];
            str += "#";
        }
        for (int i = 1; i < str.size()-1; i++) {
            // 已经不可能有更长的回文串了
            if (str.size() - i - 1 <= lens[maxCenter]) {
                break;
            }
            
            int initLen = 0;
            // i 与最右回文串有交集
            if (i < iRight) {
                // i 镜面对称点的坐标
                int iMirror = 2*iCenter-i;
                // 朴素计算的起始长度
                initLen = min(lens[iMirror], iRight - i);
            }
            
            // 综合了多情况
            lens[i] = centerSpread(str, i, initLen);
            
            // 更新最右回文串
            if (i + lens[i] > iRight) {
                iCenter = i;
                iRight = i + lens[i];
            }
            
            // 更新最长回文串的中心
            if (lens[i] > lens[maxCenter]) {
                maxCenter = i;
            }
        }
        str = str.substr(maxCenter-lens[maxCenter], 2*lens[maxCenter]+1);
        replaceAll(str, "#", "");
        return str;
    }
};
```
