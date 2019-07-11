# Share extension: couldn’t be opened because you don’t have permission to view it.

### 發生情況

當`extension`端想要對接收到的檔案的url做操作（如：`try Data(contentsOf: url)`），都會發生`Code = 257 "The file "XXX.JPG" couldn’t be opened because you don’t have permission to view it."`

####  解決方案 1

這個問題跟我的一模一樣，可惜他的解法對我無效

{% embed url="https://medium.com/%E5%BD%BC%E5%BE%97%E6%BD%98%E7%9A%84-swift-ios-app-%E9%96%8B%E7%99%BC%E6%95%99%E5%AE%A4/share-extension-couldnt-be-opened-because-you-don-t-have-permission-to-view-it-error-handling-88f7c2aea466" %}

#### 解決方案 2

這個問題跟我遇到的狀況有點相似，不過留言串很多人提供不同的方法，逐一試之

{% embed url="https://stackoverflow.com/questions/24924809/the-file-myapp-app-couldnt-be-opened-because-you-dont-have-permission-to-vi/25365372" %}



#### 解決方案 

```swift
fileURL.startAccessingSecurityScopedResource()
//...
fileURL.stopAccessingSecurityScopedResource()
```

{% embed url="https://stackoverflow.com/questions/36355105/the-file-couldn-t-be-opened-because-you-don-t-have-permission-to-view-it?rq=1" %}



