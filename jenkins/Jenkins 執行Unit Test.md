---
title: Jenkins 執行Unit Test
tags: DevOps
description:
---
# Jenkins 執行Unit Test

## Unit Test
大致上與自動建置那篇文章的建置流程大致相同(也可以把Test設定放入自動建置裡)，這篇只提出不相同處說明。

### 安裝 HTML Publisher
在jenkins首頁==Manage Jenkins==>==Plugin Manager==裡安裝(參考下圖)
![Imgur](https://i.imgur.com/8yndpIs.png)

### Build

修改Tasks改成跑Unit Test
![Imgur](https://i.imgur.com/2zVSPSU.png)

### Post-build Actions 

選擇==Publish HTML reports==
![Imgur](https://i.imgur.com/wcwLOrl.png)

設定 Html reports
![Imgur](https://i.imgur.com/EzhoWOB.png)

完成

### 測試Build

完成設定後我們可以==Build Now==執行Build看是否可以正常執行

執行結果
![Imgur](https://i.imgur.com/mB8WGcW.png)

我們可以再點擊==Html Report==查看測試結果
![Imgur](https://i.imgur.com/u8M9WOo.png)

:::danger
注意:

若Html無法正常顯示的話請在Script Console(路徑:Jenkins首頁>Manage Jenkins>Script Console)裡輸入

System.setProperty("hudson.model.DirectoryBrowserSupport.CSP", "")

如下圖
![Imgur](https://i.imgur.com/vJSpMq8.png)

點擊Run後重新Build一次Html應該就能顯示正常了
:::

參考資料:
[設定](https://medium.com/nonstopio/set-up-jenkins-for-android-continuous-integration-9ffcc70315da)
[Html 無法證正常顯示解決方法1](https://medium.com/cubemail88/devops-jenkins-html-publisher-plugin-report-%E7%84%A1%E6%B3%95%E9%A1%AF%E7%A4%BA-eeea4d7030d0)
[Html 無法證正常顯示解決方法2](https://testerhome.com/topics/9185)