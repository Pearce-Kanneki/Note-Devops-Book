---
title: Jenkins 參數說明設定
tags: DevOps
---

# Jenkins 參數說明設定

這篇說明一些流程參數說明與設定。

## General

![Imgur](https://i.imgur.com/gjHGGLA.png)

### Discard old builds

此選項配置如何拋棄舊建構

* **Days to keep builds**: 輸入值非空時，就保留輸入數值天數內的建構
* **Max # of builds to keep**: 輸入值非空時，就最多保留輸入數值個數內的建構
* **Days to keep artifacts**： 建置保留時間，但log與歷史紀錄會保留
* **Max # of builds to keep with artifacts**: 保留最近幾個構建的產品

### This project is parameterized

建置任務時，有時參數不是固定的(可能是因為有多種版本)，所以需要設置參數控制就不用每次建置時都需要重新修改，在[Jenkins 自動建置](<Jenkins 自動建置.md>)這篇我們有使用到。

![](https://i.imgur.com/JLdZAiL.png)

可參數設置種類可參考上圖，

![](https://i.imgur.com/hcm5GCe.png)

Build 任務時選擇參數

![](https://i.imgur.com/1DduGBU.png)

### Throttle builds

設定Build兩個任務之間最小間隔與同一時間內最大任務數量

### Disable this project

停止這個任務

### Execute concurrent builds if necessary

併發執行build.勾選後如果有足夠的執行緒池則會併發,否則不會，併發構建會在不同的workspace中，如果使用者自己設定的workspace則不會分開(有風險的)

### Restrict where this project can be run

設定是否必須在某個機器上執行，如果是分散式部署或者遷移job，注意移除或修改此項配置

## Build Triggers

![Imgur](https://i.imgur.com/zN15w6t.png)

### Trigger builds remotely (e.g., from scripts)

通過外部url命令觸發，並接token和url就可以進行遠端觸發了

### Build after other projects are built

監控其他任務的建構狀態觸發此任務

### Build periodically

定時觸發，使用方法與**Poll SCM**一起說

### Poll SCM

定時感知程式碼分支是否有變化，如果有變化執行一次建構\


![](https://i.imgur.com/JiTSjo4.png)

在`Schedule`裡輸入5個數字依序為

* 分: 第幾分鐘(1小時)
* 時: 第幾小時(1天)
* 日: 第幾天(1個月)
* 月: 第幾個月(1年)
* 星期: 星期幾(0、7代表星期日)

> \* 代表適用所有數字

舉例:

每天晚上10點建置

> 0 22 \* \* \*

每30分建置一次

> H/30 \* \* \* \*

週一至週五，每天的9點～18點，每隔2小時建置1次

> 0 9-18/2 \* \* 1-5

## Build Environment

![Imgur](https://i.imgur.com/SzPokmM.png)

### Delete workspace before build starts

刪除所有，也可以刪除特定檔案

* **Patterns for files to be deleted**: 用正則法刪除哪些檔案
* **Apply pattern also on directories**: 此規則是否應用到資料夾
* **Check parameter**: 是否刪除，true代表刪除反之false代表不刪除
* **External Deletion Command**: 執行外部刪除命令

### Use secret text(s) or file(s)

使用密文，用於全域性的管理密碼等。

### Abort the build if it's stuck

構建阻塞的時候根據超時處理策略

* **Time-out strategy**: 超實測略，可以選擇
  1. Absolute
  2. Deadline
  3. Elastic
  4. Likely stuck
  5. No Activity
* **Time-out variable**: 超時時間
* **Time-out actions**: 超時後處理

### Add timestamps to the Console Output

在輸出介面新增時間搓

\
參考資料:

[job介面詳解](https://www.796t.com/content/1546795810.html)
