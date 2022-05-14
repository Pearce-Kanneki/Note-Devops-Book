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

> mkdir jenkins_android

在使用者底下創立一個資料夾，等等我們會用到

### (2)ssh 連接
在`系統偏好設定`=>`共享`，開啟`遠端登入` <br>

![](https://i.imgur.com/hkwMXHR.png)

### (3)Docker container 連接
開啟Terminal，輸入下面指令
> docker container exec -it YOUR_CONTAINER_ID bash

然後按照紅色圈起處依序輸入相對應指令  
![](https://i.imgur.com/cUB2m3x.png)

## 2. 基礎設定

### Manage nodes and clouds
在`Manage Jenkins` => `Manage nodes and clouds`裡設定連線目標 <br>
先在左邊選擇`New Node`如下圖<br>
![](https://i.imgur.com/L7O6NPm.png)
<br>
輸入Node Name創立
![](https://i.imgur.com/8E689LZ.png)
<br>
在下圖輸入之前創立的資料夾位置 <br>
![](https://i.imgur.com/ImeuTeP.png)
<br>
在`Host`輸入本機IP位置，`Credentials`選擇登入帳號 <br>
![](https://i.imgur.com/M0yAdkw.png)
<br>
帳號設定可以參考本機的`系統偏好設定`=>`使用者與群組` <br>
![](https://i.imgur.com/IvD6Stu.png)
