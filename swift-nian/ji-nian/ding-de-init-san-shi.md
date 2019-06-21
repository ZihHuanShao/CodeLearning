# 關於協定的init

Protocol可以定義一個**建構器**\(即`init`方法\)，定義方法不需要寫大括號`{}`，格式如下：

```swift
protocol OtherProtocol {
    init(someParameter: Int)
}
```

### require init\(\)

如果是一個class遵循一個含有建構器的protocol時，無論是指定建構器或便利建構器，都必須為class的建構器加上`required`修飾符，以確保所有子類別也必須定義這個建構器，從而符合protocol

```swift
class OtherClass: OtherProtocol {
    required init(someParameter: Int) {
        // 建構器的內容
    }
}
```

### require override init\(\)

如果一個子類別覆寫了父類別的指定建構器，且此建構器滿足了某個協定的要求，則該建構器必須同時加上`required`和`override`

```swift
// 定義一個協定
protocol AnontherProtocol {
    init()
}

// 定義一個類別
class AnontherSuperClass {
    init() {
        // 建構器的內容
    }
}

// 定義一個繼承 AnontherSuperClass 的類別
// 同時還遵循了協定 AnontherProtocol
class SomeSubClass: AnontherSuperClass, AnontherProtocol {
    // 必須同時加上 required 和 override
    required override init() {
        // 建構器的內容
    }
}
```

