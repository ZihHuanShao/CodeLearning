# 沒有權限Share extension: couldn’t be opened because you don’t have permission to view it.

## 發生情況

當`extension`端想要對接收到的檔案的url做操作（如：`try Data(contentsOf: url)`），都會發生`Code = 257 "The file "XXX.JPG" couldn’t be opened because you don’t have permission to view it."`這邊我列出覺得可能比較有幫助的解決方法：

###  解決方案 1

這個問題跟我的一模一樣，可惜他的解法對我無效

{% embed url="https://medium.com/%E5%BD%BC%E5%BE%97%E6%BD%98%E7%9A%84-swift-ios-app-%E9%96%8B%E7%99%BC%E6%95%99%E5%AE%A4/share-extension-couldnt-be-opened-because-you-don-t-have-permission-to-view-it-error-handling-88f7c2aea466" %}

### 解決方案 2

這個問題跟我遇到的狀況不一樣，但也有點相似，留言串很多人提供不同的方法，逐一試之也都無效

{% embed url="https://stackoverflow.com/questions/24924809/the-file-myapp-app-couldnt-be-opened-because-you-dont-have-permission-to-vi/25365372" %}



### 解決方案 3

最後是這個方法能解決我的問題，在對URL操作的前後加上兩段code

```swift
fileURL.startAccessingSecurityScopedResource()
...
fileURL.stopAccessingSecurityScopedResource()
```

{% embed url="https://stackoverflow.com/questions/36355105/the-file-couldn-t-be-opened-because-you-don-t-have-permission-to-view-it?rq=1" %}

## 解決的案例

名詞解釋，以開發者角度而言：

* Extension：**接收**從其他App分享過來的檔案，以下簡稱Ext
* Containing App：將接收到的檔案做怎樣的**呈現**，以下簡稱CA

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x64CD;&#x4F5C;&#x7AEF;</th>
      <th style="text-align:left">&#x6C92;&#x6709;&#x6B0A;&#x9650;&#x7684;&#x64CD;&#x4F5C;</th>
      <th style="text-align:center">&#x6A94;&#x6848;&#x985E;&#x578B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Ext</td>
      <td style="text-align:left"><code>try? Data(contentsOf: data as! URL)</code>
      </td>
      <td style="text-align:center">&#x5716;&#x7247;</td>
    </tr>
    <tr>
      <td style="text-align:left">Ext</td>
      <td style="text-align:left">
        <p><code>let tmpData = try? Data(contentsOf: data as! URL)</code>
        </p>
        <p><code>let data = try? propertyListEncoder().encode(tmpData!)</code>
        </p>
      </td>
      <td style="text-align:center">&#x5716;&#x7247;&#x3001;Zip</td>
    </tr>
    <tr>
      <td style="text-align:left">CA</td>
      <td style="text-align:left">
        <p><code>if let shareUrl = FileManager.default.containerURL(forSecurityApplicationGroupIdentifier: yourSuiteName) {</code>
        </p>
        <p><code>  let imagePath = shareUrl.appendingPathComponent(&quot;test.JPG&quot;)</code>
        </p>
        <p><code>  let image = UIImage(contentsOfFile: imagePath.path)</code>
        </p>
        <p><code>}</code>
        </p>
      </td>
      <td style="text-align:center">&#x5716;&#x7247;</td>
    </tr>
  </tbody>
</table>

