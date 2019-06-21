# 簡易Notification機制

機制說明如下：

1. 註冊\(`addObserver`\)：**註冊**Notification，當然也需要註冊的名稱，**實作**方法來替發出通知的人做點事
2. 通知\(`post`\)：**通知**註冊者該幫我做事了
3. 移除\(`removeObserver`\)：不再使用時要移除Notification

```swift
class SecondViewController: UIViewController {
    ...
    
    // Notification的名稱
    let notificationName = NSNotification.Name(rawValue: "UpdateRecord")
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 註冊，並實作calledUpdateRecord方法
        NotificationCenter.default.addObserver(forName: notificationName, object: nil, queue: nil, using: calledUpdateRecord)
    }

    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(true)
        
        // 移除
        NotificationCenter.default.removeObserver(self, name: updateRecordNotificationName, object: nil)
    }
    
    // calledUpdateRecord方法：被通知的時候可能要幫通知者做一些資料更新的行為
    func calledUpdateRecord(notification: Notification) -> Void {
        updateDataSource()
    }
    
    func updateDataSource() {
        ...
    }
    
    ...
}
```

```swift
class FirstViewController: UIViewController {
    ...
    
    // Notification的名稱
    let notificationName = NSNotification.Name(rawValue: "UpdateRecord")
    
    // 發出通知，註冊者會自動去幫我做事
    NotificationCenter.default.post(name: notificationName, object: self, userInfo: nil)
    ...
}
```

