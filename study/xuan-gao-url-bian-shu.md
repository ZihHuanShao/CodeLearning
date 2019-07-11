# 宣告URL變數

用一般`var`的寫法會報錯，因為初始一定要帶參數

```swift
var messageURL: URL = URL()
```

正確寫法：

```swift
let url = URL(string: "https://www.apple.com")
// 或
let url:URL!
```

