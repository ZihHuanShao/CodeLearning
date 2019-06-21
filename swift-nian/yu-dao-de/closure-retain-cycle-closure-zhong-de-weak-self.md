# Closure retain cycle \(Closure中的\[weak self\]\)

### 閉包是強參考循環

除了類別實體之間可能產生強參考循環，當將一個閉包\(`closure`，也就是匿名函式\)設置給一個類別實體的屬性時，這個閉包函式內存取了這個實體的某個屬性，或是呼叫了實體的一個方法，都會導致閉包捕獲\(`capture`\)了`self`，進而產生了強參考循環。

* 閉包所捕獲的參考會被自動視為強參考。

這個強參考循環的產生，是因為閉包也是參考型別，當把閉包設置給一個屬性時，實際上是設置了閉包的參考。

解決方式請參考：

{% embed url="https://medium.com/@terryck/swift-closure-retain-cycle-906136c0b14a" %}



