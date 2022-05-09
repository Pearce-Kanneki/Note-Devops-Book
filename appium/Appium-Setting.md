---
title: Appium環境設置
tags: test
---

# Appium 安裝與設定

appium官網: https://appium.io/

Appium 是一種開源的自動化測試工具，可以測試Android、iOS和Web App，\
並且支援Python、JavaScript、Java、Ruby、C#、PHP等語言。

測試環境: MacOS\
使用語法: kotlin(實際上會走Java Client跑自動測試)\
因主要測試對象為Android App，所以不會提及到iOS和Web測試

## 安裝appium

開啟終端機並依序輸入以下指令

```
$ brew install node
$ npm install -g appium 
$ npm install wd
$ appium & 
```

* `brew install node`: 安裝node.js,如果電腦有安裝則看已跳過
* `npm install -g appium`: 安裝appium
* `npm install wd`: 安裝appium client
* `appium &` : 啟動appium

## 環境檢查

查看appium檢查工具

> appium-doctor --version

若有安裝會出現版本號，沒出現的話輸入下面指令安裝

> npm install appium-doctor -g

再來輸入指令檢查Android執行環境

> appium-doctor --android

iOS執行環境檢查指令

> appium-doctor --ios

執行結果(Android):\


![](https://i.imgur.com/EjmDZki.png)

確認哪些尚未設定或安裝，**WARN**項目可忽略。

## 檢查/安裝JAVA和Android SDK

查看目前Java jdk版本

> /usr/libexec/java\_home

執行結果:

&#x20;\
若沒安裝java則不會出現此路徑\
未安裝可去Java官網下載安裝。

![](https://i.imgur.com/lRyHDFF.png)

查看Android SDK設定

> echo $ANDROID\_HOME

執行結果:

&#x20;\
若沒安裝或設定Android SDK則不會出現此路徑\
未安裝可去Android Studio裡的SDK Manager裡選擇安裝.

![](https://i.imgur.com/geXWDun.png)

## 配置JAVA與Android環境變數

1. 在User底下新增環境設定檔

> vim \~/.bash\_profile

1. 在檔案裡輸入以下內容

```
export ANDROID_HOME=/Users/{UserName}/Library/Android/sdk
export PATH=$ANDROID_HOME/platform-tool:$PATH
export PATH=$ANDROID_HOME/tools:$PATH

export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-{version}.jdk/Contents/Home
export PATH=${PATH}$JAVA_HOME/bin
```

> 裡面內容的{UserName}請輸入自己使用者名稱\
> {version}請輸入JAVA版本

內容大概長這個樣子

![Imgur](https://i.imgur.com/9nEsO6S.png)

ps. 前面2個區塊可以忽視，那是設定flutter環境用的與本次appium環境無關。

1. 設定完之後儲存離開
2. 最後輸入下面指令執行

> source \~/.bash\_profile

ps. 此指令會執行到關機,所以電腦重開機之後需要再次執行此程式，環境才不會跑掉.

## 圖形化介面

### Appium-Desktop

#### 安裝

到官網點擊Dowload Appium或是[點擊](https://github.com/appium/appium-desktop/releases/)此處點擊下載。

當您運行它時，您可能會收到一些關於應用程序無法打開或未經 Apple 驗證或類似情況的錯誤。可參考[官方解決方法](https://github.com/appium/appium-desktop#installing-on-macos)。

#### 設定與執行

1. 開啟Appium Server GUI
2. 開啟之後點擊Edit Conigurations(如下圖)\

3. 確認是否有設定**ANDROID\_HOME**和**JAVA\_HOME**\
   配置路徑可參考**配置JAVA與Android環境變數**章節查詢路徑\

4. 配置完後儲存重啟
5. 點擊Start Serer起動

![](https://i.imgur.com/9jcqr44.png)

![](https://i.imgur.com/JbZXqZ0.png)

### Appium-Inspector

用於移動應用程序等的GUI檢查器，由Appium 服務器提供支持。你可以使用它來檢查移動應用程序

[點擊](https://github.com/appium/appium-inspector/releases)下載工具，當您運行它時，您可能會收到一些關於應用程序無法打開或未經 Apple 驗證或類似情況的錯誤。可參考[官方解決方法](https://github.com/appium/appium-desktop#installing-on-macos)
