# Activity Indicator

在網頁載入之前加入轉圈 ![](../.gitbook/assets/ying-mu-kuai-zhao-20190121-xia-wu-5.58.26%20%281%29.png) 的圖示：

1. `Library`加入 ![](../.gitbook/assets/ying-mu-kuai-zhao-20190121-xia-wu-5.49.03.png) 至`Main.storyboard`
2. 服從`WKNavigationDelegate`
3. 有兩個方法需要實作：

```swift
...

    @IBOutlet weak var myActivityIndicator: UIActivityIndicatorView!
      
    // 開始載入網頁  
    func webView(_ webView: WKWebView, didStartProvisionalNavigation navigation: WKNavigation!) {
        myActivityIndicator.startAnimating()
    }
    
    // 網頁載入完成
    func webView(_ webView: WKWebView, didFinish navigation: WKNavigation!) {
        myActivityIndicator.stopAnimating()
    }

...
```

