# TableView 顯示資料順序相反

`dialRecord`為我要顯示的資料，型態為陣列

```swift
...   
     func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let index = dialRecord.count - 1 - indexPath.row
        let cell = recentsTableView.dequeueReusableCell(withIdentifier: "RecentsCell", for: indexPath) as! RecentsTableViewCell

        cell.nameLabel.text     = self.dialRecord[index].dialName
        cell.phoneNum.text      = self.dialRecord[index].dialPhone
        cell.dialTimeLabel.text = self.dialRecord[index].dialTime
        cell.weekLabel.text     = self.dialRecord[index].dialWeek
        
        return cell
    }
...    
```

