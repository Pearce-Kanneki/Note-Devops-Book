---
title: Jenkins 通知設定
tags: DevOps
---

# Jenkins 通知設定

## Email 通知

### 設定全域config

點擊`Manage Jenkins`=>`Configure System`，往下找到`Extended E-mail Notification`\
\
這邊我使用Gmail,參數可參考(若是用gmail發送時記得`低安全應用程式存取權`需要開啟)

![](https://i.imgur.com/m3nkXB4.png)

點擊上面的`Advanced`增加發送者帳密。(可點擊`Add`增加帳號)

![](https://i.imgur.com/R7XqXbM.png)

再來就可以點擊儲存囉

### Project設定

點擊要設定的Project之後點擊`Configgure`，在`Post-build Actions`裡新增`Editable Email Notification`如下圖

![](https://i.imgur.com/T7qtDyD.png)

設定發送內容,在`Project Recipient List`裡增加發送對象(每個發送對象以`,`分開)

![](https://i.imgur.com/s9PdKIg.png)

點擊`Advanced Settings`,在點擊`Add Trigger`創立觸發時機。

![](https://i.imgur.com/0G2SWZT.png)

![](https://i.imgur.com/lusOXgo.png)

### 最後結果

![](https://i.imgur.com/cB4p2J8.png)

## Slack 通知

### Slack 建立App

點擊希望被通知的頻道名稱，選擇`整合`後`新增應用程式`

![](https://i.imgur.com/N43Nw2h.png)

搜尋`jenkins CI`,點擊`安裝`\
\


![](https://i.imgur.com/NsOTKqZ.png)

之後會開啟網頁，照著網頁做就可以囉。

### Jenkins 設定

到Jenkins裡的`Manage Jenkins`=>`Plugin Manager`確認是否有安裝`Slack Notification`

![](https://i.imgur.com/FP27cBt.png)

回到`Configure System`設定Slack

![](https://i.imgur.com/zeArkct.png)

`Workspace`輸入自己Slack URl的Doman name(可以在`編輯工作空間詳細資料`裡察看)

![](https://i.imgur.com/8UXx420.png)

依照上圖內容我們需要輸入w1624587914-cav745810，然後新增`權杖`(內容參考網頁)，注意Kind要選擇`Secret text`

![](https://i.imgur.com/LX9jATX.png)

`Default channel / member id`輸入頻道名稱，點擊`Test Connection`可以收到測試訊息。之後就可以儲存了。

![](https://i.imgur.com/wSIwStZ.png)

### Project設定

點擊要設定的Project之後點擊`Configure`，在`Post-build Actions`裡新增`Slack Notifications`如下圖\


![](https://i.imgur.com/RPaORsX.png)

選擇之後會顯示如下圖這樣，選擇觸發發送條件就可以囉。\


![](https://i.imgur.com/aTxhwi2.png)

### 最後結果

![Imgur](https://i.imgur.com/CsaxA3B.png)

## Discord 通知
Disocrd主要是給遊戲玩家使用的通訊軟體，與Slack(主要面向商業與小團隊)有些不同，使用機率也偏低，會寫這篇也是心血來潮而已。

### Webhook
點擊需要被發送的頻道按`編輯頻道`，如下圖
<br>
![Imgur](https://i.imgur.com/uSRqhHD.png)
<br>
先在左邊選擇`整合`，在點擊`查看Webhook`(若沒創立過則會顯示`建立Webhook`)
<br>
![Imgur](https://i.imgur.com/yYGNSbh.png)
<br>
創立機器人之後點擊`複製Webhook網址`，等等就會用到了
<br>
![Imgur](https://i.imgur.com/oITfcmm.png)

### Jenkins設定
到Jenkins裡的`Manage Jenkins`=>`Plugin Manager`確認是否有安裝`Discord Notifier`\
![Imgur](https://i.imgur.com/e5TP4dP.png)

### Project設定

點擊要設定的Project之後點擊`Configure`，在`Post-build Actions`裡新增`Discord Notifier`如下圖\
![Imgur](https://i.imgur.com/FGVqHfQ.png)
<br>
之後在`Webhook URL`貼上剛剛我們複製的網址\
![Imgur](https://i.imgur.com/Fv7HDpu.png)
<br>
若需要詳細設定可點擊`Advanced`

### 最終結果
![Imgur](https://i.imgur.com/pkgXcVF.png)

參考資料:

[初探Jenkins(應用)-完成動作後自動email通知](https://medium.com/on-my-way-coding/%E5%88%9D%E6%8E%A2jenkins-%E6%87%89%E7%94%A8-%E5%AE%8C%E6%88%90%E5%8B%95%E4%BD%9C%E5%BE%8C%E8%87%AA%E5%8B%95email%E9%80%9A%E7%9F%A5-657b754f2895)
