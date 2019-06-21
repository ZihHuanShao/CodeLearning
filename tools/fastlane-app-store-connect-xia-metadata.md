# \(fastlane\) 從App Store Connect下載metadata

針對要發佈的APP，想要發佈到全球的話，可以利用`fastlane`離線編輯，然後一次上傳其他國家語系的所需資訊，至App Store Connect上審查頁面中，免去線上一頁一頁填寫資料及等待的時間。

## 步驟簡述

1. 開啟終端機，安裝`fastlane`。 `# sudo gem install fastlane -NV`
2. 至自己的專案資料夾，輸入`#fastlane init`
3. 建立`fastlane`資料夾  
   `# mkdir fastlane  
   # cd fastlane/  
   # fastlane deliver init`

   驗證Apple ID與Bundle ID

4. Download existing metadata from App Store Connect，記得要先加入所有國家  
   `# fastlane deliver download_metadata`

   驗證Apple ID與Bundle ID

5. 下載screenshots

   `#fastlane deliver download_screenshots`

6. 上傳並更新至App Store Connect  
   `# fastlane deliver`

   驗證Apple ID與Bundle ID



更多詳細資訊參考連結：[https://docs.fastlane.tools/actions/deliver/](https://docs.fastlane.tools/actions/deliver/)

