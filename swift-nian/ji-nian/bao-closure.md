# 閉包Closure

列出重點特性如下，詳細及範例可參考最下方連結：

### 閉包表達式

* 是參數：可以當作函式的參數
* 是值型態：就像`X = 2`，`X`也可以是`Closure`

### 尾隨閉包 \(trailing closure\)

* 主要是增強函式的可讀性
* 當作函式參數時，若`Closure`是**唯一參數**，或者是**參數列表中的最後一個參數**，就可以將`Closure`改寫移到函式名稱後面
* 若`Closure`是**唯一參數**，甚至還可以將函式的小括號`()`刪除

### 捕獲 \(capture\)

* 意思是：在一個函式裡面再定義一個`Closure`將它回傳
* 捕獲並存取**外部函式**\(把它定義在其中的函式\)內所有的參數以及定義的常數與變數，即使這個巢狀函式已經回傳，導致常數或變數的作用範圍不存在，閉包仍能對這些已經捕獲的值做操作。 \* 感覺像是C/ C++ 在函式裡面的`static`變數

### 閉包是參考型別

* 也就是call by address

### 逃逸閉包 \(escape closure\)、非逃逸閉包 \(noescape closure\)

* **逃逸閉包**
  * `Closure`被當作函式的參數，該`Closure`會等原函式返回之後才被執行，這樣稱作`Closure`從函式中逃逸\(escape\)
* **非逃逸封包**
  * 反之，如果要明確表示一個當做參數的`Closure`不能從函式中逃逸，要在參數前標註`@noescape`。 `func someFunctionWithNoescapeClosure( @noescape closure: () -> Void) {      closure()  }`

### 自動閉包 \(autoclosure\)

* 一種自動被建立的`Closure`，用於包裝後當作函式的參數
* 這種`Closure`沒有參數
* 可以延遲求值
* 自動`Closure`含有非逃逸閉包的特性，所以你如果想讓這個`Closure`可以逃逸 ，則必須標註為`@autoclosure(escaping)`





{% embed url="https://itisjoe.gitbooks.io/swiftgo/content/ch1/closures.html\#noescape" %}



