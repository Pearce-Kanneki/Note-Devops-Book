---
title: Jenkins Build
tags: DevOps
---
# Jenkins Build

## Build
目前僅使用過Gradle，若以後有用到別的再補上

### Invoke Gradle script
先上圖
![Imgur](https://i.imgur.com/tGaF92e.png)
<br>
* Invoke Gradle: 使用自己設定好的Gradle
* Use Gradle Wrapper: 系統自己判斷需要使用哪個版本的Gradle,然後自行下載使用
* Tasks: 輸入Gradle指令位置

### Gradle 指令
#### clean
清除所有建置檔案(build相關的)

#### assemble + 版本
建置專案，assemble後面加上build類型(一般預設是Debug和Release),點擊[配置 build 變體](https://developer.android.com/studio/build/build-variants)查看說明

#### test
執行單元測試
<br>
輸出位置在`app/build/reports/tests/testDebugUnitTest/index.html`

#### connectedAndroidTest
執行UI測試
<br>
輸出位置在`app/build/reports/tests/androidTests/connected/index.html`

## Post-build Actions

### Archive the artifacts
輸出文件
<br>
![Imgur](https://i.imgur.com/4zsJ6JL.png)

### Publish HTML reports
輸出HTML報告，參考前面html位置輸出顯示html檔案
<br>
![Imgur](https://i.imgur.com/g8hmQyL.png)

