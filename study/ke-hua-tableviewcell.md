# 客製化TableViewCell

![&#x65B0;&#x589E;&#x6A94;&#x6848;&#x6642;&#x8A18;&#x5F97;&#x4E00;&#x4F75;&#x52FE;&#x9078;&#x300C;Also create XIB file&#x300D;](../.gitbook/assets/ying-mu-kuai-zhao-20190318-shang-wu-12.14.38.png)

![&#x81F3;CustomTableViewCell.xib&#xFF0C;&#x8A2D;&#x8A08;&#x8981;&#x5BA2;&#x88FD;&#x5316;&#x7684;cell&#xFF0C;&#x597D;&#x4E86;&#x8A18;&#x5F97;&#x5E6B;cell&#x53D6;ID](../.gitbook/assets/ying-mu-kuai-zhao-20190318-shang-wu-12.16.40.png)

![&#x5C07;&#x5BA2;&#x88FD;&#x5316;&#x7684;cell&#x5167;&#x5BB9;&#x9023;&#x7D50;&#x5230;CustomTableViewCell.swift](../.gitbook/assets/ying-mu-kuai-zhao-20190318-shang-wu-12.17.54.png)

![&#x9023;&#x7D50;&#x597D;&#x5C0D;&#x61C9;&#x7684;TableView&#x4E26;&#x5411;ViewController&#x8A3B;&#x518A;](../.gitbook/assets/ying-mu-kuai-zhao-20190318-shang-wu-12.27.21.png)

```swift
// nibName: 要客製化cell的檔案名稱, CustomTableViewCell.xib
// forCellReuseIdentifier: 要客製化cell的ID
myTableView.register(UINib(nibName: "CustomTableViewCell", bundle: nil), forCellReuseIdentifier: "CustomCell")
...

// withIdentifier: 要客製化cell的ID
let cell = myTableView.dequeueReusableCell(withIdentifier: "CustomCell", for: indexPath) as! CustomTableViewCell

```



![&#x986F;&#x793A;&#x5BA2;&#x88FD;&#x5316;cell&#x7684;&#x7D50;&#x679C;](../.gitbook/assets/ying-mu-kuai-zhao-20190318-shang-wu-12.34.42.png)





