# Manacher 算法



Manacher 算法可以在 $O(n)$ 时间复杂度内求出一个字符串的最长回文字串。

类似 KMP 算法：[KMP Algorithm - 字符串匹配](https://github.com/RickeyBoy/LeetCodeGists/blob/master/KMPAlgorithm.md)

基于中心扩散法：[5. Longest Palindromic Substring 最长回文子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/5LongestPalindromicSubstring.md)

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

lens[i] 的朴素计算法：中心扩散法。如果整个 lens 数组的计算全部采用中心扩散法，那么就与 [5. Longest Palindromic Substring 最长回文子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/5LongestPalindromicSubstring.md) 相同，时间复杂度为 $O(n^2)$

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


### 最右回文串 iCenter + iRight

我们维护一个已知最右的回串，设其中心点 iCenter 以及其最右点 iRight。显然两者有这么的关系:

```cpp
iRight = iCenter + lens[iCenter]。
```

那么我们维护最右回文串的意义是什么？利用回文镜像对称的特点，减少部分对 lens 的朴素计算。

比如 `OABAXABAO` 第二个 B 由于是以 X 为中心的回文串的右分支中的一部分，所以它的 lens 和第一个 B 的 lens 完全相等，也就是 lens[6] = lens[2]。

总结一下，当我们遍历 i 计算 lens[i] 的，因为 iCenter 已经遍历过，所以肯定有 i > iCenter。那么计算 lens[i] 的伪代码如下

```c++
if (i <= iRight) {
    // 在最右回串的范围内，可以应用上面的镜面复制；
    lens[i] = lens[2*iCenter-i];
} else { // i > iRight
    // 超出了最右，在未知区域，只能用朴素方式计算。
    lens[i] = centerSpread(s, i);
}
```






