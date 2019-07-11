# 取得file檔案大小

* `path`: 檔案路徑

```swift
func getSize(atPath path: String) -> UInt64? {
    do {
        // METHOD 1
        let attr = try FileManager.default.attributesOfItem(atPath: path)
        let fileSize = attr[FileAttributeKey.size] as! UInt64
            
        /*
        // METHOD 2: Old way
        let dict = attr as NSDictionary
        fileSize = dict.fileSize()
         */
            
        return fileSize
   } catch {
        print("getSize Error: \(error)")
        return nil
    }
}
```

