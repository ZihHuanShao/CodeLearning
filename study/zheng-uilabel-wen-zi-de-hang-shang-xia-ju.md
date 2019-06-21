# 調整UILabel文字的行\(上下\)間距

```swift
class ViewController: UIViewController {
    @IBOutlet weak var contentLabel: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        tuneLineSpacing(10, contentLabel)
    }
    
    func tuneLineSpacing(_ space: CGFloat, _ uiLabel: UILabel) {
        let paraph = NSMutableParagraphStyle()
        paraph.lineSpacing = space
        
        let attributes = [NSAttributedString.Key.font:UIFont.systemFont(ofSize: 15),
                          NSAttributedString.Key.paragraphStyle: paraph]
        contentLabel.attributedText = NSAttributedString(string: uiLabel.text!, attributes: attributes)
        self.view.addSubview(uiLabel)
    }    
}
```

