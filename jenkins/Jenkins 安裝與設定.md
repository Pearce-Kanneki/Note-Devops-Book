---
title: Jenkins 安裝與設定
tags: DevOps
---

# Jenkins 安裝與設定

Jenkins是由Java撰寫的開源持續整合工具，有豐富的功能可提供給開發者，可達成專案建置、測試及部署等自動化工作。

## 安裝

接下的Jenkins會裝Docker版本，所以需要一些Docker基本知識與操作，若對Docker不熟或不了解的話可能在安裝時會有不懂這個步驟在做什麼的問題(不影響Jenkins操作)。

測試環境: MacOS 其他需要的工具: Docker Jenkins Docker image說明：[Jenkins Container](https://hub.docker.com/r/jenkins/jenkins)

1.  安裝jenkins Container

    > docker pull jenkins/jenkins
2.  用下面這段指令啟動Jenkins

    > docker run --rm -u root -p 8080:8080 \ -v /Users/kannekichen/Library/Android/sdk:/usr/local/android-sdk \ -v /var/run/docker.sock:/var/run/docker.sock \ -v jenkins-data:/var/jenkins\_home \ jenkins/jenkins

等待建置中～\
&#x20;![Imgur](https://i.imgur.com/7zY33ho.png)

建制完之後會顯示以下畫面，這時我們需要到Terminal找Passwrod ![Imgur](https://i.imgur.com/PcfBTKD.png)

1. 輸入密碼到網頁中(下圖紅色圈起處貼到網頁)\
   &#x20;![Imgur](https://i.imgur.com/VooDnle.png)
2.  若無特別需求選擇==安裝推薦的外掛==就可以了\
    &#x20;![Imgur](https://i.imgur.com/mfi9t0B.png)

    安裝等待中～\
    &#x20;![Imgur](https://i.imgur.com/HwqNsmQ.png)
3. 建立管理者帳號密碼，下一步\
   &#x20;![Imgur](https://i.imgur.com/tj4HRkZ.png)
4. 設定URL(這邊我們不變更)，下一步\
   &#x20;![Imgur](https://i.imgur.com/7gBVbQJ.png)
5. 完成囉\
   &#x20;![Imgur](https://i.imgur.com/igt8WyA.png)

## 環境設定

### 設定Android Home

1. 在Jenkins首頁點選`Manage Jenkins`\
   &#x20;![Imgur](https://i.imgur.com/rsWujym.png)
2. 再點選 `Configure Sytem`\
   &#x20;![Imgur](https://i.imgur.com/SGs2sKd.png)
3. 在`Global properties`裡設定Android\_Home 圖片修正中
