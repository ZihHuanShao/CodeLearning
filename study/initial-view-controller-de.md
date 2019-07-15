# initial view controller的選擇

## 設計情景

第一次啟動APP ➡︎ `FirstViewController`  
已登入過APP ➡︎ `SecondViewController`

使用一組`key`來判斷是否有登入過, 並在`AppDelegate.swift`裡的`didFinishLaunchingWithOptions`加入判斷式

{% code-tabs %}
{% code-tabs-item title="AppDelegate.swift" %}
```swift
...
    
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    
        if UserDefaults.standard.bool(forKey: "FLAG_LOGIN") {
            self.window = UIWindow(frame: UIScreen.main.bounds)
            let storyboard = UIStoryboard(name: "Main", bundle: nil)
            
            let initialViewController = storyboard.instantiateViewController(withIdentifier: "NavigationOfViewController") // 選擇哪個VC
            
            self.window?.rootViewController = initialViewController
            self.window?.makeKeyAndVisible()
        }
        
        return true
    }

...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

