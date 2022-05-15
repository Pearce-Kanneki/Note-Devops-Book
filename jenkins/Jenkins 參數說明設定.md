---
title: Jenkins 參數說明設定
tags: DevOps
---

# Jenkins 參數說明設定
這篇說明一些流程參數說明與設定。

## General

### Discard old builds

此選項配置如何拋棄舊建構
- **Days to keep builds**: 輸入值非空時，就保留輸入數值天數內的建構
- **Max # of builds to keep**: 輸入值非空時，就最多保留輸入數值個數內的建構
- **Days to keep artifacts**： 建置保留時間，但log與歷史紀錄會保留
- **Max # of builds to keep with artifacts**: 保留最近幾個構建的產品

### This project is parameterized
建置任務時，有時參數不是固定的(可能是因為有多種版本)，所以需要設置參數控制就不用每次建置時都需要重新修改，在[Jenkins 自動建置](Jenkins%20自動建置.md)這篇我們有使用到。
<br>
![Imgur](https://i.imgur.com/JLdZAiL.png)
<br>

可參數設置種類可參考上圖，\\

![Imgur](https://i.imgur.com/hcm5GCe.png)
<br>
Build 任務時選擇參數
<br>
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

參考資料: <br>
[job介面詳解](https://www.796t.com/content/1546795810.html)