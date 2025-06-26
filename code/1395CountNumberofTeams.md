### [1395. Count Number of Teams](https://leetcode.cn/problems/count-number-of-teams/)

There are `n` soldiers standing in a line. Each soldier is assigned a **unique** `rating` value.

You have to form a team of 3 soldiers amongst them under the following rules:

- Choose 3 soldiers with index (`i`, `j`, `k`) with rating (`rating[i]`, `rating[j]`, `rating[k]`).
- A team is valid if: (`rating[i] < rating[j] < rating[k]`) or (`rating[i] > rating[j] > rating[k]`) where (`0 <= i < j < k < n`).

Return the number of teams you can form given the conditions. (soldiers can be part of multiple teams).

 

**Example 1:**

```
Input: rating = [2,5,3,4,1]
Output: 3
Explanation: We can form three teams given the conditions. (2,3,4), (5,4,1), (5,3,1). 
```

**Example 2:**

```
Input: rating = [2,1,3]
Output: 0
Explanation: We can't form any team given the conditions.
```

**Example 3:**

```
Input: rating = [1,2,3,4]
Output: 4
```

 

**Constraints:**

- `n == rating.length`
- `3 <= n <= 1000`
- `1 <= rating[i] <= 105`
- All the integers in `rating` are **unique**.



### 解法：

```swift
class Solution {
    func numTeams(_ rating: [Int]) -> Int {
        // calculate large to small cases:
        // 1. smaller[i]: count of smallers in the right
        // 2. larger[i]: count of largers in the left
        // 3. larger[i] * smaller[i] => combinations that use i as the second!
        let n = rating.count
        var result = 0
        for i in (1..<n-1) {
            let leftPart = rating.prefix(i)
            let rightPart = rating[i+1..<n]
            let smallInLeft = leftPart.count { $0 < rating[i] }
            let largeInRight = rightPart.count { $0 > rating[i] }
            result += smallInLeft*largeInRight
            let smallInRight = rightPart.count - largeInRight
            let lergeInLeft = leftPart.count - smallInLeft
            result += lergeInLeft*smallInRight
            // print("center number \(rating[i]), lergeInLeft \(lergeInLeft), smallInLeft \(smallInLeft), smallInRight \(smallInRight), largeInRight \(largeInRight)")
        }
        return result
    }
}
```