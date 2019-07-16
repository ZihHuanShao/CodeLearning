# share extension implement

## Study progress ...

{% hint style="warning" %}
遇到的瓶頸：只要對來源檔案的`url`做處理，就會發生沒有權限可以操作的狀況
{% endhint %}

item = 來源檔案，App端 = Container App

1. **處理端 = 接收端\(extension\)**  逐一針對每一個item的type做相對應的處理，然後一個一個寫進Group space  EX：分享網頁➔存網址、圖片➔轉`Data`存或直接寫入圖片檔 
2. **處理端 = 呈現端\(App端\)**  建立一個`struct`物件，將所有item的資訊（`url`、`name`、`type`、`size`）存到該物件，再一次寫進Group space 
3. **回到沒有權限問題** 
4. **解決3後再回到2.** 有寫入權限但App端沒有讀檔權限 
5. **解決3.後再回到1.** App端順利讀檔

## **1. 處理端 = 接收端\(extension\)**

接收端會針對每一個item做資料處理，處理完再寫入Group space

### 寫入方式`UserDefaults.init(suiteName: "YourSuiteName")`

* 測項：網頁URL

  * `userDefault?.set(url, forKey: "url")`➔ 成功寫入

  **讀取端**：成功讀取✅

* 測項：圖片
  * 轉成`Data`型別寫入：`let imageData = try? Data(contentsOf: url)`➔ 沒有權限操作 **讀取端**：None 
  * 轉成`Data`型別，再透過`PropertyListEncoder().encode`編碼再寫入➔ 可以寫入。但有時會無法寫入並顯示沒有權限操作 **讀取端**：若順利寫入可以成功讀取✅❎

```swift
let tmpData = try? Data(contentsOf: data as! URL)
let data = try? propertyListEncoder().encode(tmpData!)

// userDefault?.set(value: Any?, forKey: String)
userDefault.set(data!, forKey: "image")
```

* 測項：其他類型檔案如ZIP檔
  * 轉成`Data`型別，再透過`PropertyListEncoder().encode`編碼再寫入➔ 沒有權限操作 **讀取端**：None 

### 寫入方式`FileManager.default.containerURL(forSecurityApplicationGroupIdentifier: "YourSuiteName")`

* 測項：圖片
  * 直接寫入圖片檔➔ 成功寫入 **讀取端**：沒有權限讀取❎

```swift
let tmpData = try? Data(contentsOf: url)
let imagePath = shareUrl.appendingPathComponent(url.lastPathComponent)
try? tmpData!.write(to: imagePath)
```

## 2. **處理端 = 呈現端\(App端\)**

主要讓App端去對item做資料處理，所以接收端這邊就不針對item做處理，而是取得每一個item的**檔名**、**檔案類型**、**URL**、**檔案大小**並存到自己的`struct`物件`FileObject`，然後再將這所有的物件存到一個`FileObject`陣列，最後再把陣列一次寫入到Group space，然後等待App端取得後再處理

* `FileObject`物件資訊如下

```swift
struct FileObject: Codable {
    let name: String
    let type: ContentType
    let url:  URL
    let size: UInt64
}
```

### 寫入方式`UserDefaults.init(suiteName: "YourSuiteName")`

* 蒐集到的每一筆item物件全部存到一個陣列，再透過對陣列的編碼，寫到Group space➔ 成功寫入 **讀取端**：成功讀取✅

```swift
try? PropertyListEncoder().encode(data as! [FileObject])

// userDefault?.set(value: Any?, forKey: String)
userDefault!.set(data, forKey: storeKey)
```

雖然讀取成功，嘗試要對物件的URL操作的才話，一樣會發生沒有權限讀取的問題。

## 3. 回到沒有權限問題

因為先前嘗試了幾種讀寫方式，雖然上述有成功讀寫的案例，但也不可靠，根本問題還是因為沒有權限`"The file "XXX.JPG" couldn’t be opened because you don’t have permission to view it."`，所以改朝這個方向去解決

{% page-ref page="untitled.md" %}

因此，最後解決方法是在對URL操作的前後加上兩段code

```swift
fileURL.startAccessingSecurityScopedResource()
...
fileURL.stopAccessingSecurityScopedResource()
```

## 4. 解決3.後再回到2.

讀取端一樣能夠讀取成功。但對`FileObject`取出來的URL操作時，一樣沒有權限可以使用

## 5. **解決3.後再回到1.**

### 寫入方式`UserDefaults.init(suiteName: "YourSuiteName")`

* 測項：圖片

  * 轉成`Data`型別寫入，`let imageData = try? Data(contentsOf: url)`➔ 成功寫入沒有權限操作 **讀取端**：讀取成功✅

  在解決沒有寫入權限問題後，單純轉成`Data`型別就可以寫入了，也不用特地對item做編碼才能寫入

### 寫入方式`FileManager.default.containerURL(forSecurityApplicationGroupIdentifier: "YourSuiteName")`

* 測項：圖片
  * 直接寫入圖片檔➔ 成功寫入 **讀取端**：成功讀取✅

## 目前作法

同時保留第1種及第2種方式：

* 第2種：**處理端 = 呈現端\(App端\)**

  在接收端利用`FileObject`物件陣列，來當作在App端顯示所有資料的依據

* 第1種：**處理端 = 接收端\(extension\)** 因為item的URL必須在接收端處理，所以就不同類型的檔案必須先做資料處理，處理完寫入Group space

