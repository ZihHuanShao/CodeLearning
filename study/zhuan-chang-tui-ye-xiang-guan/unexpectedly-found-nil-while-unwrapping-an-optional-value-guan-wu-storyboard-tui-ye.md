# Unexpectedly found nil while unwrapping an Optional value 關於storyboard推頁

## 使用情境

在實作`UITableViewDelegate`的`didSelectRowAt`方法時，目的是在`Main.storyboard`裡的`ViewController`底下的`TableView`選到哪一個`cell，`就會跳到另一個`InfoView.storyboard`上的`InfoViewController.swift`並顯示我要的資訊。

{% code-tabs %}
{% code-tabs-item title="InfoViewController.swift" %}
```swift
class InfoViewController: UIViewController {

    @IBOutlet weak var testLabel: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="ViewController.swift" %}
```swift

class ViewController: UIViewController {
    @IBOutlet weak var myTableView: UITableView!    

    override func viewDidLoad() {
        super.viewDidLoad()
        
        myTableView.delegate = self
        myTableView.dataSource = self
    }
}
...

extension ViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let storyBoard = UIStoryboard(name: "InfoView", bundle: nil)
        let infoVC = storyBoard.instantiateViewController(withIdentifier: "InfoViewController") as! InfoViewController
        infoVC.testLabel.text = "Hello World"
        self.navigationController?.pushViewController(infoViewController, animated: true)
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 現在使用情形

在swift 3時使用上述方法還能正常執行。但不知道何時被改掉了，現在只要執行到`infoVC.testLabel.text = "Hello World"`這段就會報錯：`Unexpectedly found nil while unwrapping an Optional value`

\`\`

## `解決方法`

在`InfoViewController.swift`多加一個全域變數就可以了。原來只要多繞一小圈就可以了，當初還卡一小段時間，下面附上參考連結

{% code-tabs %}
{% code-tabs-item title="InfoViewController.swift" %}
```swift
class InfoViewController: UIViewController {

    @IBOutlet weak var testLabel: UILabel!
    
    // ⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎
    var testString: String!

    override func viewDidLoad() {
        super.viewDidLoad()

        self.testLabel.text = testString
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="ViewController.swift" %}
```swift
...

extension ViewController: UITableViewDelegate {
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let storyBoard = UIStoryboard(name: "InfoView", bundle: nil)
        let infoViewController = storyBoard.instantiateViewController(withIdentifier: "InfoViewController") as! InfoViewController
        
        // ⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎⬇︎
        infoViewController.testString = "Hello World"
        
        self.navigationController?.pushViewController(infoViewController, animated: true)
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed url="https://stackoverflow.com/questions/28741399/iboutlet-of-another-view-controller-is-nil" %}



