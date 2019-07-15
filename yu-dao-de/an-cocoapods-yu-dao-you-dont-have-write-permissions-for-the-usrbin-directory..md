# 安裝cocoapods遇到You don't have write permissions for the /usr/bin directory.

#### 問題

指令：`sudo gem install cocopods`

結果：`ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /usr/bin directory.`

####  解決方法

改用此指令： `sudo gem install cocoapods -n /usr/local/bin`

{% embed url="https://www.jianshu.com/p/b8406ff1e2f1" %}



