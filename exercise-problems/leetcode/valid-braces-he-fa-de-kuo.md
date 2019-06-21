# \#20. Valid Parentheses

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```text
Input: "()"
Output: true
```

**Example 2:**

```text
Input: "()[]{}"
Output: true
```

**Example 3:**

```text
Input: "(]"
Output: false
```

**Example 4:**

```text
Input: "([)]"
Output: false
```

**Example 5:**

```text
Input: "{[]}"
Output: true
```

驗證是否為合法的括號

## Think

使用堆疊的概念

| 測試字串`"[({}[()])]"` |
| :--- |
| `[ -> [` |
| `( -> [ (` |
| `{ -> [ ( {` |
| `} -> [ ( { } pop -> [ (` |
| `[ -> [ ( [` |
| `( -> [ ( [ (` |
| `) -> [ ( [ ( ) pop -> [ ( [` |
| `] -> [ ( [ ] pop -> [ (` |
| `) -> [ ( ) pop -> [` |
| `] -> [ ] pop => return true` |

## Solution

```swift
func isValid(_ s: String) -> Bool {
    let mappingTable:[Character:Character] = [")": "(",
                                              "]": "[",
                                              "}": "{"]
    var arr = Array(s)
    var newArr = [Character]()
    var offset = 0
    
    if arr.isEmpty { return true }
    
    // The amount of arr must be even
    if arr.count % 2 != 0 { return false }
    
    // Start is invalid, like ), ], }
    if mappingTable[arr[0]] != nil { return false }
    
    for i in 0..<arr.count {        
        newArr.append(arr[i])
        if i == 0 { continue }
        if let map = mappingTable[newArr[i - offset]] {
            if map == newArr[i - offset - 1] {
                newArr.removeLast()
                newArr.removeLast()
                offset += 2
            }
        }
    }
    
    if !newArr.isEmpty { return false }
    
    return true
}

// test...
isValid("(){}[]")
isValid("(}")
isValid("[(])")
isValid("([{}])")

```

## Question Ref.

{% embed url="https://leetcode.com/problems/valid-parentheses/" %}



