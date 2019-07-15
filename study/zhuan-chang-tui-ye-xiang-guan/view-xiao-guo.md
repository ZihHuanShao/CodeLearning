# View 轉場效果

## View轉場方法

1. 透過`UIStoryboard()`取得我要轉場到哪個`ViewController`（必須先設定好這個`ViewController`的`Storyboard Id`，這邊是取得我自行設定`Storyboard Id`為**`lightRed`**的`ViewController`\)
2. 選擇使用`present()`或`pushViewController()`來套用效果

```swift
// 初始化View Controller
let lightRed = UIStoryboard(name: "Main", bundle: nil).instantiateViewController(withIdentifier: "lightRed")
        
// 由下至上顯示
present(lightRed, animated: true, completion: nil)
        
// 由左至右顯示
// ** 若要使用此種顯示方式，必須先將當前的View Controller嵌入Navigation Controller
// ** Editor> Embed In> Navigation Controller
navigationController?.pushViewController(lightRed, animated: true)
```

## 另一種轉場方法: `segue`

透過`segue`來設定，圖中左邊箭頭指的地方就代表`segue`，右邊可以設定該`segue`的名稱。再使用`performSegue()`要呈現哪個`segue`來套用。

![](../../.gitbook/assets/tu-pian-1%20%281%29.png)

```swift
// 1. 由下至上顯示

// 2. 由左至右顯示
// ** 若要使用此種顯示方式，必須先將當前的View Controller嵌入Navigation Controller
// ** Editor> Embed In> Navigation Controller


// 上述兩種顯示方式都使用以下的方法，差別只是在於第2種必須嵌入Navigation Controller
performSegue(withIdentifier: "gotoView2", sender: nil)
```

## 返回的方法

* 轉場效果為`present()`，返回上一頁使用`dismiss()`

```swift
// 返回上一頁
dismiss(animated: true, completion: nil)
```

* 轉場效果為`pushViewController()`，返回上一頁使用`popViewController`或返回首頁`popToRootViewController()`

```swift
// 返回上一頁
super.navigationController?.popViewController(animated: true)

// 返回第一個畫面
super.navigationController?.popToRootViewController(animated: true)
```

