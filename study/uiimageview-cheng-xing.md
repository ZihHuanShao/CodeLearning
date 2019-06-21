# 讓UIImageView變成圓形

```swift
...
   @IBOutlet weak var userImage: UIImageView!
   
...
   override func viewDidAppear(_ animated: Bool) {
      super.viewDidAppear(animated)
      
      userImage.layer.cornerRadius = userImage.frame.size.width / 2
      userImage.clipsToBounds = true
   }
...
```

