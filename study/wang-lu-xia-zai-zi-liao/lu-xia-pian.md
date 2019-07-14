# 網路下載資料1. Data

使用`Data()`下載圖片：

```swift
...

    @IBOutlet weak var myImageView: UIImageView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        let imageAddress = "https://pay.google.com/about/static/images/social/knowledge_graph_logo.png"
        if let imageURL = URL(string: imageAddress){
            do{
                myImageView.image = UIImage(data: try Data(contentsOf: imageURL))
            }catch{
                print(error.localizedDescription)
            }
        }
    }
    
...
```

如上例所示，若下載的圖片很大，此時我想做別的操作，這樣會導致螢幕整個卡住。  
因此改為下列作法：

```swift
...
    
    @IBOutlet weak var myImageView: UIImageView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        let imageAddress = "https://pay.google.com/about/static/images/social/knowledge_graph_logo.png"
        if let imageURL = URL(string: imageAddress){
            DispatchQueue.global().async {
                do{
                    let downloadImage = UIImage(data: try Data(contentsOf: imageURL))
                    DispatchQueue.main.async {
                        self.myImageView.image = downloadImage
                    }
                }catch{
                    print(error.localizedDescription)
                }
            }
        }
    }
    
...
```

