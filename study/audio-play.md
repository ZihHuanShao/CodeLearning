# Audio play 音訊播放功能

{% hint style="info" %}
 播放音訊需要使用到`AVAudioPlayer`這個類別
{% endhint %}

1. 建立Project
2. 匯入mp3音檔 \(直接拖曳檔至XCODE視窗即可\)
3. 取得音檔路徑
4. 產生`AVAudioPlayer()`

{% hint style="info" %}
`AVAudioPlayer()`使用`throws`的方法， 操作時記得加入`do`、`try`、`catch`![](../.gitbook/assets/wei-ming-ming%20%282%29.png) 
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="ViewController.swift" %}
```swift
import UIKit
import AVFoundation //使用Audio功能必須匯入AVFoundation

class ViewController: UIViewController {
    
    var audioPlayer:AVAudioPlayer?
    
    @IBAction func play(_ sender: UIButton) {
        audioPlayer?.play()
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 取得路徑
        if let audioPath = Bundle.main.path(forResource: "Right", ofType: "mp3"){
           
             // 取得URL
            let url = URL(fileURLWithPath: audioPath)
            
            do{
                audioPlayer = try AVAudioPlayer(contentsOf: url)
            }catch{
                print(error.localizedDescription)
            }
        }else{
            print("no such file")
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

列出常用的`AVAudioPlayer()`的幾個功能：

```swift
//要改變播放音樂速度的話必須先enable
audioPlayer?.enableRate = true 
//慢0 ~ 快2.0
audioPlayer?.rate = 0.5        

//反覆播放2次
audioPlayer?.numberOfLoops = 2

//無限制反覆播放
audioPlayer?.numberOfLoops = -1

//音量大小
audioPlayer?.volume = 0.3

//停止播放
audioPlayer?.stop()
//播放時間重新設定為開頭(0)
audioPlayer?.currentTime = 0.0
//播放
audioPlayer?.play()
```

參考`AVAudioPlayer()`函式的其他屬性：[https://developer.apple.com/documentation/avfoundation/avaudioplayer](https://developer.apple.com/documentation/avfoundation/avaudioplayer)

{% embed url="https://developer.apple.com/documentation/avfoundation/avaudioplayer" %}

