# View Life Cycle 視圖生命週期

`View`是`ViewController`類別的其中一個屬性，可以將`View`看作成整個程式畫面。

| View的其他方法 | 說明 |
| :---: | :---: |
| `loadView` | 用程式碼產生畫面 |
| `viewDidLoad` | 讀入畫面之後執行 |
| `viewWillAppear` | 畫面即將顯示到螢幕上 |
| `viewDidAppear` | 畫面已經顯示到螢幕上 |
| `viewWillDisappear` | 畫面即將離開螢幕 |
| `viewDidDisappear` | 畫面已經離開螢幕 |

為了能夠更了解畫面跟程式執行的先後關係，首先先建立一個Project並在以下幾支檔加入`print()`訊息來追蹤：

{% code-tabs %}
{% code-tabs-item title="ViewController.swift" %}
```swift
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        print("view: did load")
    }
    
    override func loadView() {
        super.loadView()
        print("view: load view")
    }
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        print("view: did recieve memory wraning")
    }
        
    override func viewWillAppear(_ animated: Bool) {
        print("view: will appear")
    }
    
    override func viewDidAppear(_ animated: Bool) {
        print("view: did appear")
    }
    
    override func viewWillDisappear(_ animated: Bool) {
        print("view: will disappear")
    }
    
    override func viewDidDisappear(_ animated: Bool) {
        print("view: did disappear")
    }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="AppDelegate.swift" %}
```swift
import UIKit

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        print("app: did finish launch")
        return true
    }
    
    func applicationWillResignActive(_ application: UIApplication) {
        print("app: will resign active")
    }
    
    func applicationDidEnterBackground(_ application: UIApplication) {
        print("app: did enter background")
    }
    
    func applicationWillEnterForeground(_ application: UIApplication) {
        print("app: will enter foreground")
    }
    
    func applicationDidBecomeActive(_ application: UIApplication) {
        print("app: did become active")
    }
    
    func applicationWillTerminate(_ application: UIApplication) {
        print("app: will terminate")
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>View</code>&#x6A21;&#x5F0F;</th>
      <th style="text-align:left">&#x57F7;&#x884C;&#x7D50;&#x679C;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x5F9E;&#x4E3B;&#x756B;&#x9762;&#x9EDE;&#x9078;&#x5716;&#x793A;&#x555F;&#x52D5;App</td>
      <td
      style="text-align:left">
        <p><b><code>app: did finish launch</code></b>
        </p>
        <p><b><code>view: load view</code></b>
        </p>
        <p><b><code>view: did load</code></b>
        </p>
        <p><b><code>view: will appear</code></b>
        </p>
        <p><b><code>view: did appear</code></b>
        </p>
        <p><b><code>app: did become active</code></b>
        </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">App&#x57F7;&#x884C;&#x4E2D; -&gt; &#x61F8;&#x6D6E;&#x8996;&#x7A97;</td>
      <td
      style="text-align:left"><b><code>app: will resign active</code></b>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">App&#x57F7;&#x884C;&#x4E2D; -&gt; &#x61F8;&#x6D6E;&#x8996;&#x7A97;<b> </b>-&gt;
        &#x56DE;&#x5230;App&#x756B;&#x9762;</td>
      <td style="text-align:left">
        <p><b><code>app: will resign active</code></b>
        </p>
        <p><b><code>app: did become active</code></b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">App&#x57F7;&#x884C;&#x4E2D; -&gt; (&#x6309;home&#x9375;)&#x56DE;&#x5230;&#x4E3B;&#x756B;&#x9762;</td>
      <td
      style="text-align:left">
        <p><b><code>app: will resign active</code></b>
        </p>
        <p><b><code>app: did enter background</code></b>
        </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x4E3B;&#x756B;&#x9762; -&gt; &#x61F8;&#x6D6E;&#x8996;&#x7A97;</td>
      <td
      style="text-align:left">none</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x4E3B;&#x756B;&#x9762; -&gt; &#x61F8;&#x6D6E;&#x8996;&#x7A97; -&gt;
        &#x56DE;&#x5230;App&#x756B;&#x9762;</td>
      <td style="text-align:left">
        <p><b><code>app: will enter foreground</code></b>
        </p>
        <p><b><code>app: did become active</code></b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">App&#x57F7;&#x884C;&#x4E2D; -&gt; &#x61F8;&#x6D6E;&#x8996;&#x7A97;<b> </b>-&gt;
        &#x95DC;&#x9589;App</td>
      <td style="text-align:left">
        <p><b><code>app: will resign active</code></b>
        </p>
        <p><b><code>app: did enter background</code></b>
        </p>
        <p><b><code>app: will terminate</code></b>
        </p>
      </td>
    </tr>
  </tbody>
</table>下面圖示：透過轉場到另一個新增的View controller，就可以看出下面的執行狀況了

![](../.gitbook/assets/image%20%2812%29.png)

{% embed url="https://developer.apple.com/documentation/uikit/uiviewcontroller" %}



![](../.gitbook/assets/image%20%288%29.png)

{% embed url="https://medium.com/@ChunYeung/swift-%E8%AB%87%E8%AB%87%E5%B9%BE%E5%80%8B%E9%87%8D%E8%A6%81%E7%9A%84-ios-app-life-cycle-%E7%94%9F%E5%91%BD%E9%80%B1%E6%9C%9F-93380fe93d95" %}



