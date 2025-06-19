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
```

### 常见操作

- string

```cpp
tolower(char)\toupper(char)  // 将字符进行大小写转换
s.insert(s.begin(),'a') // 插入
s.erase(s.begin()+first,s.begin()+last) // 删除字符串中迭代器区间 [first, last) 上所有字符
s.find("abc") // 查找一个字符串
s.substr(first, length) // 子串
reverse(s.begin(), s.end());              // 字符串反转
s.length() / s.size();                    // 获取字符串长度
#include <string>
std::string s = std::to_string(-42) // int 转换成 String
stoi(s); // 字符串转 int
```

- vector

```cpp
vector<int> v1;                        // 空 vector
vector<int> v2(5);                     // 长度为 5，默认值为 0
vector<int> v3(5, -1);                 // 长度为 5，初始值为 -1
v.push_back(x);                    // 添加元素
v.pop_back();                      // 删除最后一个元素
v.size();                          // 元素个数
v.clear();                         // 清空
v.empty();                         // 是否为空
// reverse
reverse(a.begin(), a.end());
// sort 从小到大
sort(myvector.begin(), myvector.begin()+4);
// sort 自定义比较
sort(v.begin(), v.end(), greater<int>()); // 从大到小
bool myfunction (int i,int j) { return (i<j); } // using function as comp
sort (myvector.begin()+4, myvector.end(), myfunction);
// sum
#include <numeric>
cout << accumulate(A.begin(), A.end(), 0);
```

- stack

```c++
stack<int> s;
s.empty()               // 如果栈为空返回 true，否则返回 false  
s.size()                // 返回栈中元素的个数  
s.top()                 // 返回栈顶元素的值，但不删除该元素  
s.pop()                 // 删除栈顶元素，但不返回其值  
s.push(x)               // 向栈顶压入新元素 x  
```

- queue

```cpp
queue<int> q;
q.empty()               // 如果队列为空返回true，否则返回false
q.size()                // 返回队列中元素的个数
q.pop()                 // 删除队列首元素但不返回其值
q.front()               // 返回队首元素的值，但不删除该元素
q.push()                // 在队尾压入新元素
q.back()                // 返回队列尾元素的值，但不删除该元素
```

- Unoredered_map

```cpp
unordered_map<string, int> m1;
int n = map.count('z');  // 判断元素是否存在【不是个数】，n == 1 代表存在
map.find(key) == map.end() // 判断元素是否不存在, true 即不存在
```

- Set

```cpp
unordered_set<int> us;    // 平均常数时间，支持存在性判断
s.insert(x);
s.erase(x);
s.count(x);               // 是否存在（0或1）
s.find(x) == s.end();     // 判断不存在
```

- Priority_queue

```cpp
priority_queue<int> pq; // 默认大顶堆
priority_queue<int, vector<int>, greater<int>> pq; // 小顶堆
// 存 Node 节点的小顶堆
struct compare {
	bool operator()(ListNode* a, ListNode* b) {
		return a->val > b->val; // 小顶堆，val 小的优先
	}
};
priority_queue <ListNode*, vector<ListNode*>, compare> queue; 
// Basics
pq.push(x) // 插入元素
pq.top() // 返回当前队首元素（最大/最小）
pq.pop() // 弹出队首元素（并不返回值）
pq.empty() //是否为空
pq.size() //当前队列元素个数
```

- 位运算

```cpp
x & 1        // 判断奇偶（1为奇）
x << 1       // 左移，相当于 x * 2
x >> 1       // 右移，相当于 x / 2
x ^ y        // 异或（相同为 0，不同为 1）
x | y        // 按位或
~x           // 取反
x &= ~(1<<k) // 将第 k 位清零
x |= (1<<k)  // 将第 k 位设为 1
```

