# 按下return移到下個文字欄位

1. 須遵從`UITextFieldDelegate`協定
2. 替每個文字欄位給定`tag`值，依序遞增
3. 複寫`textFieldShouldReturn`方法

```swift
class ViewController: UIViewController, UITextFieldDelegate {
    ...
    
    @IBOutlet weak var name1: UITextField! {
        didSet {
            name1.tag = 1
            name1.becomeFirstResponder()
            name1.delegate = self
        }
    }
    
    @IBOutlet weak var phone1: UITextField! {
        didSet {
            phone1.tag = 2
            phone1.delegate = self
        }
    }
    
    @IBOutlet weak var name2: UITextField! {
        didSet {
            name2.tag = 3
            name2.delegate = self
        }
    }
    
    @IBOutlet weak var phone2: UITextField! {
        didSet {
            phone2.tag = 4
            phone2.delegate = self
        }
    }
    
    ...
    
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        if let nextTextField = view.viewWithTag(textField.tag + 1) {
            name1.resignFirstResponder()
            nextTextField.becomeFirstResponder()
        }
        return true
    }
}
```

