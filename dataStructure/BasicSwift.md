# 数据结构基础代码

### 初始化

```swift
// 数组
var arr = [1, 2, 3]
var emptyArr: Int = []
var fixedArr = Array(repeating: 0, count: 10)
// 集合
var set: Set<Int> = [1, 2, 3]
// 字典
var dict: [String: Int] = ["a": 1, "b": 2]
var emptyDict = [Int: String]()
```

### 常见操作

- Character

```swift
let ch: Character = "a"
let ascii = ch.asciiValue! // UInt8
let val = Int(ascii - Character("a").asciiValue!) // 转成 0~25
Character("1").isNumber // 判断是否为数字
```

- Array / String

```cpp
arr.count         // 返回元素个数
arr.isEmpty       // 是否为空
arr.remove(at: 2)      // 删除下标为 2 的元素
arr.insert(42, at: 1)  // 在下标 1 插入元素 42
arr.contains(3)            // 是否包含某元素
arr.firstIndex(of: 3)      // 返回第一个匹配的索引（Optional）
for (i, val) in arr.enumerated() {} // 带下标遍历
arr.sort()         // 升序（原地）
arr.sort(by: >)    // 降序（原地）
arr.max() || arr.min()  // 查找最大/最小
arr.prefix(3)                  // 前 3 个元素
arr.suffix(2)                  // 后 2 个元素
// 字符串转数组、数组转字符串
let chars = Array(str)           // ["a", "b", "c"]
let joined = chars.joined()      // "abc"
s.reversed() // 翻转
```

- Array Slice

```swift
// 数组切片
let sub = arr[1..<3]  // 注意返回的是 ArraySlice<Int>
// 字符串切片
let s = "leetcode"
let start = s.index(s.startIndex, offsetBy: 2)
let end = s.index(s.startIndex, offsetBy: 5)
let substr = String(s[start..<end]) // 从 index 2 到 4
```

- Dict

```cpp
// 遍历
for (key, val) in dict { }
```
