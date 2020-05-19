### 面试题09. 用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )



示例 1：

输入：
```
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
示例 2：

输入：
```
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```
提示：
```
1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```

### 解法

两个栈，分别存储正序和逆序
添加只在正序栈，删除只在逆序栈
只在必要时才交换栈数据，避免两个连续的删除指令需要多次来回交换

``` cpp
class CQueue {
    // 每一时刻只会有一个栈中有数据
    stack<int> order; // 正序存储队列元素
    stack<int> reversed; // 逆序存储队列元素
public:
    CQueue() {

    }
    
    void appendTail(int value) {
        // 如果数据在逆序栈中，先将逆序栈倒序加入正序栈中，再 push
        if(!reversed.empty()) {
            while(!reversed.empty()) {
                order.push(reversed.top());
                reversed.pop();
            }
        }
        // 保证数据在正序栈中，直接 push 即可
        order.push(value);
    }
    
    int deleteHead() {
        // 如果数据在正序栈中，需要先倒序加入逆序栈
        if(!order.empty()) {
            while(!order.empty()) {
                reversed.push(order.top());
                order.pop();
            }
        }
        // 如果逆序栈中没数据，返回-1
        if(reversed.empty()) return -1;
        // 保证数据在逆序栈中，此时 pop 相当于在正序中 deleteHead
        int v = reversed.top();
        reversed.pop();
        return v;
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```