# 轉場後回到上一頁，所選擇項目的底色不會消失

解決**轉場後回到上一頁，所選擇項目的底色不會消失**的問題

```swift
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    tableView.deselectRow(at: indexPath, animated: true)
}
```

