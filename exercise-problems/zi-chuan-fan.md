# 字串反轉

### 字串反轉之1

使用內建`reversed`函式

```swift
var str = "Life is always struggle"

String(str.reversed())
// 或
String(str.characters.reversed())
```

印出`elggurts syawla si efiL`

### 字串反轉之2

1. 先將字串轉成陣列
2. 陣列元素對調
3. 轉回字串

```swift
var str = "Life is always struggle"
func reverseString(_ s: String) -> String {
    // 1.
    var stringArr = Array(s)
    
    // 2.
    var i = 0
    var j = stringArr.count - 1
    while i < j {
        var temp = stringArr[i]
        stringArr[i] = stringArr[j]
        stringArr[j] = temp
        i += 1
        j -= 1
    }
    
    // 3.
    return String(stringArr)
}
reverseString(str)
```

印出`elggurts syawla si efiL`

### 字串按照句子反轉

1. 先將字串轉成陣列
2. 利用`map`將陣列裡的每個元素\(字串\)做反轉
3. 轉回字串

```swift
var str = "Life is always struggle"

func reverseString(_ s: String) -> String {
    // 1.
    let parts = s.split(separator: " ") // 1.
    
    // 2.
    let reversedStr = parts.map({
        String($0.reversed())
    })
    
    // 3.
    return reversedStr.joined(separator: " ")
}
reverseString(str)
```

印出`efiL si syawla elggurts`

