---
title: Jenkins 通知設定
tags: DevOps
---

# Jenkins 通知設定

## Email 通知

### 設定全域config

點擊`Manage Jenkins`=>`Configure System`，往下找到`Extended E-mail Notification`\
\
這邊我使用Gmail,參數可參考(若是用gmail發送時記得`低安全應用程式存取權`需要開啟)&#x20;

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

最後結果

![](https://i.imgur.com/cB4p2J8.png)
