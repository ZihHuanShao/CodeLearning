# \#66. Plus One

Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

**Example 1:**

```text
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example 2:**

```text
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

給定一個陣列存放非負整數，第一個元素不可為0，將整個陣列視為一數值，加1並傳回

## Think

### About Solution1

1. 把值從陣列取出並加1
2. 存回陣列

=&gt; 此方法若在測試的值過大時，因為當中有轉型成`Int()`，會發生`build error: Float value cannot be converted to Int because the result would be greater than Int.max`

### About Solution2

1. 陣列最後的元素加1，並存回原位置
2. 若陣列中包含`10`，則進位。將該值變為零，依序向前一個值加1
3. 遇到陣列元素皆為9的，如`[9, 9, 9]`，建立一個新陣列並存1進去，再把原本處理完的陣列`append`進去新陣列

## Solution1

```swift
func plusOne(_ digits: [Int]) -> [Int] {
    var powOfTen = digits.count - 1
    var sum      = 0
    
    for num in digits {
        sum      = (num % 10) * Int(powf(10, Float(powOfTen))) + sum
        powOfTen -= 1
    }
    sum      = sum + 1
    var res  = [Int]()
    var quot = sum
    var mod  = 0
    repeat {
        mod = quot % 10
        quot = quot / 10
        res.append(mod)
    } while quot != 0
    
    return res.reversed()
}

// test....
plusOne([9,9,9]) // success
plusOne([7,2,8,5,0,9,1,2,9]) // success
plusOne([7,2,8,5,0,9,1,2,9,5,3,6,6,7,3,5,7,9,5,6]) // error
```

## Solution2

```swift
func plusOne(_ digits: [Int]) -> [Int] {
    var digits = digits
    digits[digits.count - 1] += 1
    
    while digits.contains(10) {
        let i = digits.lastIndex(of: 10)!
        digits[i] = 0
        if i - 1 >= 0 {
            digits[i - 1] += 1
        } else {
            var newArr = [1]
            newArr.append(contentsOf: digits)
            digits = newArr
        }
    }
    return digits
}

// test...
plusOne([9,9,9]) // success
plusOne([7,2,8,5,0,9,1,2,9]) // success
plusOne([7,2,8,5,0,9,1,2,9,5,3,6,6,7,3,5,7,9,5,6]) // success
```

## Question Ref.

{% embed url="https://leetcode.com/problems/plus-one/" %}



