# share ext study

## Study & Testing

item = 來源檔案，App端 = Container App 

1. **處理端 = 接收端\(extension\)**  逐一針對每一個item的type做相對應的處理，然後一個一個寫進Group space  EX：分享網頁➔存網址、圖片➔轉data存或直接寫入圖片檔
2. **處理端 = 呈現端\(App端\)**  建立一個struct物件，將所有item的資訊（url、name、type）存到該物件，再一次寫進Group space
3. 解沒有權限問題
4. 解決3後再試2.，有寫入權限但App端沒有讀檔權限
5. 解決3後再試1.，App端順利讀檔

### 

### **1. 處理端 = 接收端\(extension\)**

接收端會針對每一個item做資料處理，處理完再寫入Group space



#### `UserDefaults.init(suiteName: "YourSuiteName")` 

* 測項：網頁URL 

  *  `userDefault?.set(url, forKey: "url")`➔ 成功寫入

  **讀取端**：成功讀取✅

* 測項：圖片
  * 轉成`Data`型別寫入，`let imageData = try? Data(contentsOf: url)`➔ 沒有權限操作
  * 轉成`Data`型別，再透過`PropertyListEncoder().encode`編碼再寫入➔ 可以寫入，但有時會無法寫入，並顯示沒有權限操作 `let tmpData = try? Data(contentsOf: data as! URL) let data = try?  PropertyListEncoder().encode(tmpData)` **讀取端**：若順利寫入可以成功讀取✅❎
* 測項：其他類型檔案如ZIP檔
  * 轉成`Data`型別，再透過`PropertyListEncoder().encode`編碼再寫入➔ 沒有權限操作



#### `FileManager.default.containerURL(forSecurityApplicationGroupIdentifier: "group.maxkit.fred.ShareExtensionTest")`

* 測項：圖片

  * 直接寫入圖片檔➔ 成功寫入 `let imagePath = shareUrl.appendingPathComponent(url.lastPathComponent)  try? UIImage(named: url.lastPathComponent)?.jpegData(compressionQuality: 1)?.write(to: imagePath)` **讀取端**：沒有權限讀取❎

### 2. **處理端 = 呈現端\(App端\)**

主要讓App端去對item做資料處理，所以接收端這邊就不針對item做處理，而是取得每一個item的檔名、檔案類型、URL並存到自己的struct物件，然後再將這所有的物件存到一個陣列，將陣列一次寫入到Group space，然後等待App端取得後再處理

* 蒐集到的每一筆item物件全部存到一個陣列，再透過對陣列的編碼`try? PropertyListEncoder().encode(data as! [FileObject])`，使用`UserDefaults.init(suiteName: "YourSuiteName")`方式寫到Group space➔ 成功寫入 **讀取端**：成功讀取✅

雖然讀取成功，但是嘗試要對物件的URL操作的才話，一樣會發生沒有權限讀取的問題。

