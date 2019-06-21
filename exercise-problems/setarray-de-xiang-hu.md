# Set與Array的相互轉換

若需要將陣列中重複的元素刪除掉，可利用`Set`的操作特性\(用來儲存**相同型別且沒有順序、沒有重複的值**\)先消除重複元素，再使用`Array()`轉換成陣列做後續的處理。

```swift
var arr:[Int] = [-1, 0, 1, 2, -1, -4] // [-1, 0, 1, 2, -1, -4]
var arrToSet:Set<Int> = Set(arr)      // {-1, 2, 0, 1, -4}
var setToArr:[Int] = Array(arrToSet)  // [-1, 2, 0, 1, -4]
```

```swift
let mySet:Set<String> = Set(["a", "b", "a"])  // {"a", "b"}
let myArray:[String] = Array(mySet)           // ["a", "b"]
```

```swift
var t1 = [[1, 1, 1], [2, 2, 2], [1, 1, 1]] // [[1, 1, 1], [2, 2, 2], [1, 1, 1]]
var t2:Set<[Int]> = Set(t1)                // {[2, 2, 2], [1, 1, 1]}
var t3:[[Int]] = Array(t2)                 // [[2, 2, 2], [1, 1, 1]]
```

