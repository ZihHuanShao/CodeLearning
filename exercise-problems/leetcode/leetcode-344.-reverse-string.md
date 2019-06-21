# \#344. Reverse String

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

**Example 1:**

```text
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```text
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

## Solution1

```swift
func reverseString(_ s: inout [Character]) {
    s.reverse()
}

// test...
var s1: [Character] = ["h","e","l","l","o"]
var s2: [Character] = ["H","a","n","n","a","h"]
reverseString(&s1)
reverseString(&s2)
```

## Solution2

```swift
func reverseString(_ s: inout [Character]) {
    var i = 0
    var j = s.count - 1
    var tmp:Character = " "
    while i < j {
        tmp = s[i]
        s[i] = s[j]
        s[j] = tmp
        i += 1
        j -= 1
    }
}

// test...
var s1: [Character] = ["h","e","l","l","o"]
var s2: [Character] = ["H","a","n","n","a","h"]
reverseString(&s1)
reverseString(&s2)
```

## Question Ref.

{% embed url="https://leetcode.com/problems/reverse-string/" %}



