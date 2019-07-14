# UserDefaults存取自訂型別

{% hint style="danger" %}
雖然`UserDefaults`能夠存放`Any`型別，但並不是所有型別都能接受，即便轉了Data格式但在寫入時又會發生錯誤，最主要得透過`PropertyListEncoder`和`PropertyListDecoder`的方式來存取。
{% endhint %}



之前很納悶為什麼單純寫入時會一直出現error，很疑惑也找不出解決之道，找了很久終於發現這篇文章，感謝作者^^

作者頁面的`struct`要注意，需加上遵循`Codable`：

```swift
struct User: Codable {
    var ID: String
    var name: String
    var email: String?
}
```

{% embed url="https://archie.tw/2018/08/15/userdefaults-with-structure/" %}



