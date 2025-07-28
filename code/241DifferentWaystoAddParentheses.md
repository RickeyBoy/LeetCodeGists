### [241. Different Ways to Add Parentheses](https://leetcode.cn/problems/different-ways-to-add-parentheses/)

Given a string `expression` of numbers and operators, return *all possible results from computing all the different possible ways to group numbers and operators*. You may return the answer in **any order**.

The test cases are generated such that the output values fit in a 32-bit integer and the number of different results does not exceed `104`.

**Example 1:**

```
Input: expression = "2-1-1"
Output: [0,2]
Explanation:
((2-1)-1) = 0 
(2-(1-1)) = 2
```

**Example 2:**

```
Input: expression = "2*3-4*5"
Output: [-34,-14,-10,-10,10]
Explanation:
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```

### 解法：递归

```cpp
class Solution {
    func calculate(_ l: Int, _ r: Int, _ op: Character) -> Int {
        if op == Character("-") {
            return l-r
        } else if op == Character("+") {
            return l+r
        } else {
            return l*r
        }
    }
    func diffWaysToCompute(_ expression: String) -> [Int] {
        // recursion func:
        // meet operators: search left + search right, then get results
        // no operators: pure number
        // print("searching: \(expression)")

        let operators: [Character] = ["-", "+", "*"]
        let expressionArray = Array(expression)

        var results: [Int] = []
        var hasOperators = false
        for idx in (0..<expressionArray.count) {
            let c = expressionArray[idx]
            if operators.contains(c) {
                hasOperators = true
                let leftResult = diffWaysToCompute(String(expressionArray[0..<idx]))
                let rightResult = diffWaysToCompute(String(expressionArray[idx+1..<expressionArray.count]))
                for l in leftResult {
                    for r in rightResult {
                        results.append(calculate(l, r, c))
                    }
                }
            }
        }
        if !hasOperators {
            // pure number
            return [Int(expression)!]
        }
        return results
    }
}
```
