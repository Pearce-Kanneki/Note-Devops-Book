---
title: Appium 執行測試
tags: test
description: appium 測試工具說明
---

# Appium 執行測試

假如測試APK時沒有原始碼要如何測試呢？我們可以使用Appium來看Android APK元件屬性，這些屬性會是我們撰寫自動化程式碼UI元件依據。

## Appium Inspector 開啟與設定

開啟Appium Inspector出現下圖畫面\
&#x20;

![](https://i.imgur.com/VBZVymH.png)

注意: 若Appium非2.0版本則必須在紅色框框內輸入`/wd/hub`，2.0版本則是`/`(也可以不輸入)，詳細說明請看[官方說明](https://github.com/appium/appium-inspector#important-migration-notes)

再來我們需要對右邊的JSON 輸入以下範本(部分內容需使用者修改)

```json
{
  "platformName": "Android",
  "automationName": "UiAutomator2",
  "autoGrantPermissions": true,
  "deviceName": "{Device_Name}",
  "app": "{APK_path}"
}
```

* platformName: 測試平台，輸入Android就可以了
* automationName: testing framework測試名稱，官方推薦`UiAutomator2`
* autoGrantPermissions: 是否同意系統授權
* deviceName: 手機/模擬器名稱，可以利用adb devices查看
* app: apk放置路徑

輸入後會大概長這個樣子\


![](https://i.imgur.com/PDKe2Gs.png)

最後點擊右下角的**Start Session**就能查看元素了\
ps.在點擊之前確認Appium Service和手機/虛擬機是否有啟動。

最後結果:\


![](https://i.imgur.com/WGlHUOv.png)

## 查看Android UI 元素

### UI介面說明

接下來簡單說明介面有哪些功能\
&#x20;

![](https://i.imgur.com/92gbnPl.png)

左邊是App上面的畫面(也就是實機畫面)，中間則是畫面的Source Code(未必是工程師寫的Code，像這個專案我是用Jetpack Compose畫出來的與這邊顯示的Code差異很大)，右邊則是被選的元件詳細資料(這邊資料很重要等等我們要寫的Code會參考這邊)。

## 開啟新的Test專案

這邊我們不使用Android Studio撰寫Code，要使用IntelliJ來撰寫，兩邊的介面大致相同(畢竟Android Studio是基於IntelliJ為Android開發特殊客製化出來的)可以很快地上手。

> 這邊我們不使用Android Studio開發的理由有2個
>
> * 我們不是開發Android App所以不用特定使用Android Studio開發
> * 撰寫此Code的身份可能不是RD，可能是QC確保產品品質而撰寫出來的



`下面的操作可能因版本不同而按鍵或流程不同，參考就好`

1. 首先我們點擊 **New Project** 開啟新專案\
   &#x20;
2. 再來New Project，專案名稱與存放位置自己決定，Languge選Kotlin，Build system選Gradle，剩下的不用調整我們可以點Create開啟專案囉!\
   &#x20;
3.  點擊build.gradle後找到`repositories`加入下面的程式碼

    ```groovy
    maven { url 'https://jitpack.io' }
    ```

    再往後找到`dependencies`加入

    ```groovy
    testImplementation 'junit:junit:4.13.2'
    implementation 'com.github.appium:java-client:7.3.0'
    ```

    我們需要使用junit撰寫Test Code,使用java-client連接appium
4. 同步專案

![](https://i.imgur.com/CUIVp7G.png)

![](https://i.imgur.com/BgZzqGx.png)
