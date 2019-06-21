# UIImageView & UIImage

{% hint style="info" %}
`UIImageView`可當作相框

`UIImage`可當作相片
{% endhint %}

```swift
 ...
   @IBOutlet weak var myPet: UIImageView!

    override func viewDidLoad() {
        super.viewDidLoad()
        myPet.image = UIImage(named: "Cat")
    }
...
```

