---
title: Jenkins 執行UI Test
tags: DevOps
---

# Jenkins 執行UI Test

## UI Test

建置流程與Unit Test差不多，但我們必須多一些額外設定，讓測試可以執行

## 1.ssh 與本機連接

這次測試流程我們需要連接測試機(實體機或虛擬機)，但docker無法直接連接測試機，所以我們必須連接到本機在連接測試機。

### (1)本機創立資料夾

> mkdir jenkins\_android

在使用者底下創立一個資料夾，等等我們會用到

### (2)ssh 連接

在`系統偏好設定`=>`共享`，開啟`遠端登入`\


![](https://i.imgur.com/hkwMXHR.png)

### (3)Docker container 連接

開啟Terminal，輸入下面指令

> docker container exec -it YOUR\_CONTAINER\_ID bash

然後按照紅色圈起處依序輸入相對應指令\


![](https://i.imgur.com/cUB2m3x.png)

## 2. 基礎設定

### Manage nodes and clouds

在`Manage Jenkins` => `Manage nodes and clouds`裡設定連線目標\
先在左邊選擇`New Node`如下圖\


![](https://i.imgur.com/L7O6NPm.png)

&#x20;輸入Node Name創立

![](https://i.imgur.com/8E689LZ.png)

\
在下圖輸入之前創立的資料夾位置

![](https://i.imgur.com/ImeuTeP.png)

\
`Launch method`選擇`Launch agents via SSH`，在`Host`輸入本機IP位置，`Credentials`選擇登入帳號

![](https://i.imgur.com/M0yAdkw.png)

帳號設定可以參考本機的`系統偏好設定`=>`使用者與群組`

![](https://i.imgur.com/IvD6Stu.png)

可以點擊`Add`新增帳號會出現如下圖畫面，輸入相關資料後儲存之後就可以了<br>
![Imgur](https://i.imgur.com/8tkSaKP.png)
<br>
在`Host Key Verification Strategy`這邊設定如下圖<br>
![Imgur](https://i.imgur.com/fk8IGJ5.png)
<br>
`SSH Key`可以從下圖方式找到<br>
![Imgur](https://i.imgur.com/5uuKpBp.png)
<br>
這樣我們Node就設置好了

### Global properties
在`Manage Jenkins`=>`Configure System`裡我們需要多設一組Android SDK設定，因為到時候跑設定會走本機的設定，位置就設本機Android SDK位置，見下圖 <br>
![Imgur](https://i.imgur.com/naVbAFe.png)

## 3. 流程設置
流程跟前2篇差不多，這邊ㄧ樣只說明不ㄧ樣的地方。

### General
這邊我們要選擇`Restrict where this project can be run`，然後選擇剛剛設定的Nodes如下圖 <br>
![Imgur](https://i.imgur.com/T1ikmxf.png)

### Gradle
因為這次我們要跑UI Test所以指令有些許不圖，見下圖。 <br>
![Imgur](https://i.imgur.com/cN4Nh9J.png)

### Publish HTML reports
輸出Html位置與Unit Test不同所以需要修改位置。 <br>
![Imgur](https://i.imgur.com/g8hmQyL.png)
<br>
這樣就完成囉，接上測試機就可以Build Now了

## 4.結果
輸出結果<br>
![Imgur](https://i.imgur.com/93RGdV7.png)
<br>
我們可以看到UI Test的Test數量比Unit Test少但測試時間比多很多(這邊會顯示30是因為我接了3台測試機所以測試數量會提高3倍)<br>
![Imgur](https://i.imgur.com/Wh80C5F.png)
<br>
隨便點擊任一class可以看到各測試機執行時間與Passed百分比<br>
![Imgur](https://i.imgur.com/DOioUK9.png)
<br>
![Imgur](https://i.imgur.com/9BZSyHt.png)