# Files App \(Import files\)

## 前言

### 蘋果提供統一型別的規範：UTI

因應檔案類型在不同環境可能會有不同名稱，像`.jpg`、`.jpeg`、`JPEG`、`image/jpeg`，這些檔其實都屬於同一種類型，蘋果就把這些檔案歸納為`public.jpeg`型別，這是一種**UTI**型別，也就是APPLE為了方便統一管理所有檔案，制定了**UTI \(Uniform Type Identifiers\)**型別，讓自己所有APPLE的裝置都能夠方便相互存取

{% embed url="https://developer.apple.com/library/archive/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html" caption="更多UTI型別參考" %}

### 取得檔案的UTI型別

我們應該都知道`.jpg`、`.jpeg`、`JPEG`等這些格式都屬於UTI型別的`Public.jpeg`，但若我們不知道某檔案的UTI型別時該怎麼辦呢？像是`.plist`檔是屬於何種型別該怎麼判別？

#### 方法

在指令列輸入 `mdls -name kMDItemContentType 你的檔案`，回傳結果就是UTI型別

{% embed url="https://eclecticlight.co/2018/01/24/file-types-the-uti-and-even-more-metadata/" caption="參考方法" %}

另外，在XCode底下若要使用`kUTTypeXXXX`，必須要`import MobileCoreServices`才能取得

## File Provider：作為一個提供者的角色

* 允許其他APP使用`UIDocumentPickerViewController`類別來取得裝置內部的所有資料，並會將選擇的資料匯入到此APP中，這也代表該資料會被複製一份，而原始檔則確保不會被更動到
* 另外，也允許其他APP直接開啟所選擇的檔案，像圖檔、影音檔這些通常都能夠直接開啟，但若選擇的檔案較特別，就要看有沒有其他APP有支援

