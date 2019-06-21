# \#345. Reverse Vowels of a String

Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**

```text
Input: "hello"
Output: "holle"
```

**Example 2:**

```text
Input: "leetcode"
Output: "leotcede"
```

將字串裡的母音反轉

## Think

1. 將字串轉為字串陣列，建立母音的Table\(包含大小寫\)
2. 建立新陣列，存放字串當中的所有母音，存完後反轉陣列
3. 依序走訪原字串陣列，若當下元素為母音，則替換剛建立的陣列
4. 轉為字串回傳

## Solution

```swift
func reverseVowels(_ s: String) -> String {
    let vowelSet: Set<Character> = ["a", "e", "i", "o", "u", "A", "E", "I", "O", "U"]
    var sArr        = Array(s)
    var vowelArr    = [Character]()
    var vowelIndex  = 0

    for i in sArr {
        if vowelSet.contains(i) { vowelArr.append(i) }
    }

    vowelArr.reverse()

    for i in 0..<sArr.count {
        if vowelSet.contains(sArr[i]) {
            sArr[i] = vowelArr[vowelIndex]
            vowelIndex += 1
        }
    }
    return String(sArr)
}
```

## Question Ref.

{% embed url="https://leetcode.com/problems/reverse-vowels-of-a-string/" %}



