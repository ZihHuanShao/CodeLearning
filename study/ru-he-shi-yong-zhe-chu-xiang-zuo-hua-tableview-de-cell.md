# 如何讓使用者刪除\(向左滑\)TableView的Cell

1. 實作

   ```swift
   func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath)
   ```

2. 判斷式 `if editingStyle == .delete`
3. 移除完元素之後，記得要再重新寫入資料，資料才會更新
4. `reloadData`讓TableView畫面更新

```swift
extension RecentsContainerViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        if editingStyle == .delete {
            myData.remove(at: indexPath.row)
            UserDefaults.standard.set(myData, forKey: "myData")
            myTableView.reloadData()
        }
    }
}
```

