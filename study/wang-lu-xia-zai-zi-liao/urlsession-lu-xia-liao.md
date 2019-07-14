# 網路下載資料2. URLSession

{% hint style="info" %}
`URLSession`下載工作預設都在**共時\(**global\)**佇列**下載
{% endhint %}

要從網路上透過`URLSession`類別下載資料，有兩種方法：

### `dataTask`

```swift
    var sesssion = URLSession?
    
    ...    
        // 建立URLSession
        session = URLSession(configuration: .default)
        
        // URL：要從哪個網站下載資料
        // completionHandler：下載完成後要處理的事情
        //  - Data：下載完的data
        //  - URLResponse：連結網站時的回應，比如404 Not Found
        //  - Error：過程中產生的錯誤訊息
        let task = session?.dataTask(with: URL, completionHandler: (Data?, URLResponse?, Error?) -> Void)
        
        // 開始下載資料，下載完成回到上述的completionHandler執行工作
        task?.resume()
    ...
...
```

網路下載圖片範例：

```swift
...
    var session: URLSession?
    
    override func viewDidLoad() {
        super.viewDidLoad()
        session = URLSession(configuration: .default)
        let imageAddress = "https://pay.google.com/about/static/images/social/knowledge_graph_logo.png"
        if let imageURL = URL(string: imageAddress){
            let task = session?.dataTask(with: imageURL, completionHandler: {
                (data, response, error) in
                if error != nil{
                    print(error!.localizedDescription)
                    return
                }
                if let loadedData = data{
                    let loadedImage = UIImage(data: loadedData)
                    DispatchQueue.main.async {
                        self.myImageView.image = loadedImage
                    }
                }
                
            })
            task?.resume()
        }
    }
...
```

### **`downloadTask`**

```swift
    var sesssion = URLSession?
    
    ...    
        // 建立URLSession
        session = URLSession(configuration: .default)
        
        // URL：要從哪個網站下載資料
        // completionHandler：下載完成後要處理的事情
        //  - URL：下載完存放在手機的某個URL位置
        //  - URLResponse：連結網站時的回應，比如404 Not Found
        //  - Error：過程中產生的錯誤訊息
        let task = session?.downloadTask(with: URL, completionHandler: (URL?, URLResponse?, Error?) -> Void)
        
        // 開始下載資料
        task?.resume() 
    ...
...
```

網路下載圖片範例：

```swift
...
    var session: URLSession?
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        session = URLSession(configuration: .default)
        
        let url = URL(string: "https://pay.google.com/about/static/images/social/knowledge_graph_logo.png")!
        let task = session?.downloadTask(with: url, completionHandler: {
            (url, response, error) in
            if error != nil {
                print(error?.localizedDescription)
                return
            }
            if let loadedURL = url {
                do{
                    let loadedImage = UIImage(data: try Data(contentsOf: loadedURL))
                    DispatchQueue.main.async {
                        self.myImageView.image = loadedImage
                    }
                }
                catch {
                    print(error.localizedDescription)
                }
            }
        })
        
        task?.resume()
    }
...
```

### 進階的錯誤處理

```swift
...
         if error != nil{
            
            // 轉型成NSError再呼叫code成員可以抓取錯誤的代碼。如-1009為沒有網路時的錯誤代碼
            let errorCode = (error! as NSError).code
            if errorCode == -1009{
                print("no internet connection")
            }else{
                print(error!.localizedDescription)
            }
            return
        }
...
```







外部參數`withXMLAddress`為要解析的網頁且型別為字串，範例：

```swift
func downloadXML(withXMLAddress xmlAddress:String){
    if let url = URL(string: xmlAddress){
        let task = session.dataTask(with: url) {
            (data, response, error) in
            if error != nil {
                print(error!.localizedDescription)
                return
            }
            if let okData = data{
                // 直接印出會顯示網頁內容大小(Byte)
                //print(okData)
                    
                // 透過編碼解析來呈現網頁實際內容
                print(NSString(data: okData, encoding: String.Encoding.utf8.rawValue))
            }
        }
        task.resume()
    }    
  }
```

