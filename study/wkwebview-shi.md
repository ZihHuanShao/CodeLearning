# WKWebView 顯示網頁

## 顯示網頁

1. 需要使用**WebKit View** Library
2. 匯入函式庫`import WebKit`
3. 在Info.plist加入以下key![](../.gitbook/assets/wei-ming-ming%20%286%29.png)設成yes

## 範例

{% code-tabs %}
{% code-tabs-item title="ViewController.swift" %}
```swift

class ViewController: UIViewController{

    @IBOutlet weak var myWebView: WKWebView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        if let url = URL(string: "https://www.apple.com"){
            let request = URLRequest(url: url)
            myWebView.load(request)
        }
    }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

