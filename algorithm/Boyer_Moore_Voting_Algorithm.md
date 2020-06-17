# 摩尔投票算法

### 说明

- 目的：求众数
- 原理：每次从序列里选择两个不相同的数字删除掉（或称为“抵消”），最后剩下一个数字或几个相同的数字，就是出现次数大于总数一半的那个
- 做法：每次删除两个不相同的数字
- 拓展：求超过[1/3]的数，做法每次删除三个不相同的数字

### 相关的题目：

[169. Majority Element 多数元素](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/169MajorityElement.md) - easy

[229. Majority Element II 求众数 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/229MajorityElementII.md) - medium