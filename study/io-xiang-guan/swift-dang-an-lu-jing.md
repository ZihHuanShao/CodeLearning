# Swift檔案路徑

## Sandbox的Document資料夾

### Method 1

```swift
let url = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first!

print(url)
```

印出

`file:///var/mobile/Containers/Data/Application/BFA0F0C2-CF9A-44D0-89AC-44BA17E7647C/Documents/`

### Method 2

```swift
let path = NSHomeDirectory() + "/Document"
let url = URL(fileURLWithPath: path)

print(url)`
```

印出

`file:///var/mobile/Containers/Data/Application/BFA0F0C2-CF9A-44D0-89AC-44BA17E7647C/Document`

#### Method 3

```swift
let documentPath = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0]

print(documentPath)
```

印出，反而沒有`file://`前贅字會印出

`/var/mobile/Containers/Data/Application/BFA0F0C2-CF9A-44D0-89AC-44BA17E7647C/Documents`

## 列出Document底下所有的檔案

必須使用**沒有**`file://`前贅字的路徑去取檔名，可使用前述的 Method 3先取得Document路徑

```swift
// Use Method 3 to get Document path
let documentPath = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0]

do{
    let fileList = try FileManager.default.contentsOfDirectory(atPath: documentPath)
    for file in fileList{
        print(file)
    }
catch{
    print("Cannot list directory")
}
```

印出（結果僅為範例）

```swift
店面圖片.7z
筆記.pages
apple_tv_privacy_policy.txt
UnzipReadme.zip
text.txt
1.png
```

