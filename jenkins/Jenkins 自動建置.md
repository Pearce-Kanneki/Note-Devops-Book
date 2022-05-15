---
title: Jenkins 自動建置
tags: DevOps
---

# Jenkins 自動建置

當開發者將程式碼提交合併到儲存庫時，我們希望Jenkins能幫助我們檢查程式碼是否能編譯成功，你可以馬上發現錯誤。下面開始說明如何設定。

## 建立自動建置

### 1. 新增專案

點擊`New Item`開啟新專案

![](https://i.imgur.com/bQkunNf.png)

輸入專案名稱，點擊`Freestyle project`

![](https://i.imgur.com/0UZoduq.png)

點擊OK繼續建立

### 2. General 設定

點選`This project is parameterized`

![](https://i.imgur.com/rDVuSBm.png)

選擇`Choice Parameter`增加參數

![](https://i.imgur.com/Uu9pjM5.png)

接下來這些參數會在後面或者以後會用到\\

![Imgur](https://i.imgur.com/hcm5GCe.png)

### 3. Source Code Management

在這個區塊選擇git，並在Repository Url填入Git Repository，若Git是非公開的需要新增一組帳號。下面選擇愈Build的分支。

![](https://i.imgur.com/8UELiVn.png)

### 4. Build Trigger

設定完成Code儲存庫路徑後，可以在`Builder Trigger`設定，
<br>
設定方式可參考[Jenkins 參數說明設定](<jenkins/Jenkins 參數說明設定.md>)

### 5. Build 構建設定

選擇`Invoke Gradle script`

![Imgur](https://i.imgur.com/anW7yqq.png)

設定Gradle參數

![](https://i.imgur.com/8bkLpUW.png)

> BUILD\_TYPE 參考General 設定

### 6. Post-build Actions 構建後行為設定

在Post-build Actions

![](https://i.imgur.com/C7JFjDx.png)

選擇`Archive the artifacts`

![](https://i.imgur.com/xayduoH.png)

設定參數`app/build/outputs/apk/` 或 `**/*.apk`

![](https://i.imgur.com/o0lRq6R.png)

完成設定

### 7.建構測試

先選擇`Build with Parameters`， 然後再右邊選參數設定後Build\


![](https://i.imgur.com/1DduGBU.png)

等待建置

![Imgur](https://i.imgur.com/a3OIGHW.png)

建置成功

![Imgur](https://i.imgur.com/iUoOhIM.png)

點擊之後可以看到以下畫面

![Imgur](https://i.imgur.com/VuospuT.png)

> Console Output: 可以看構建的細節

參考資料:

[Android Jenkins](https://medium.com/evan-android-note/jenkins-bb11f371bcb6)

[docker jenkins](https://www.gushiciku.cn/pl/gmfI/zh-tw)
