# 数据结构基础代码

### 头文件

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    return 0;
}
```



### 数据结构声明

```cpp
// 链表
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};
// 二叉树
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
// 小顶堆
struct compare {
	bool operator()(ListNode* a, ListNode* b) {
		return a->val > b->val;
	}
};
priority_queue <ListNode*, vector<ListNode*>, compare> queue; 
// 大顶堆
priority_queue <int> q;
```



### 常见操作

- string

```cpp
tolower(char)\toupper(char)  // 将字符进行大小写转换
s.insert(s.begin(),'a') // 插入
s.erase(s.begin()+first,s.begin()+last) // 删除字符串中迭代器区间 [first, last) 上所有字符
s.find("abc") // 查找一个字符串
s.substr(first, length) // 子串
#include <string>
std::string s = std::to_string(-42) // int 转换成 String
```

- vector

```cpp
// reverse
reverse(a.begin(), a.end());
// sort 从小到大
sort (myvector.begin(), myvector.begin()+4); // using default comparison (operator <):
// sort 自定义比较
bool myfunction (int i,int j) { return (i<j); } // using function as comp
sort (myvector.begin()+4, myvector.end(), myfunction);
// sum
#include <numeric>
cout << accumulate(A.begin(), A.end(), 0);
```

- stack

```c++
s.empty()               // 如果栈为空返回 true，否则返回 false  
s.size()                // 返回栈中元素的个数  
s.top()                 // 返回栈顶元素的值，但不删除该元素  
s.pop()                 // 删除栈顶元素，但不返回其值  
s.push(x)               // 向栈顶压入新元素 x  
```

- queue

```cpp
q.empty()               // 如果队列为空返回true，否则返回false
q.size()                // 返回队列中元素的个数
q.pop()                 // 删除队列首元素但不返回其值
q.front()               // 返回队首元素的值，但不删除该元素
q.push()                // 在队尾压入新元素
q.back()                // 返回队列尾元素的值，但不删除该元素
```

- Unoredered_map

```cpp
int n = map.count('z');  // 判断元素是否存在【不是个数】，n == 1 代表存在
map.find(key) == map.end() // 判断元素是否不存在, true 即不存在
```

- 位运算

```cpp
& 与 ^ 异或 | 或 ~ 取反 << 左移 >> 右移
```

