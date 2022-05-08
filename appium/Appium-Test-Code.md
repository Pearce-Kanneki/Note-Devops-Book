---
title: Appium Test Code
tags: test
description:
---
# Appium Test Code

首先我們先在test裡新增一個Test Class，在Class加入下面的function。  

```kotlin
    fun getAppiumDriver(): AndroidDriver<MobileElement> {

        val capabilities = DesiredCapabilities().apply {
            setCapability(MobileCapabilityType.PLATFORM_NAME, MobilePlatform.ANDROID)
            setCapability(MobileCapabilityType.DEVICE_NAME, "Pixel 5 API 29")
            setCapability(AndroidMobileCapabilityType.AUTO_GRANT_PERMISSIONS, true)
            setCapability(MobileCapabilityType.AUTOMATION_NAME, AutomationName.ANDROID_UIAUTOMATOR2)
            setCapability(MobileCapabilityType.APP, "/Users/kannekichen/Desktop/app.apk")
        }
        return AndroidDriver(URL("http://127.0.0.1:4723/wd/hub"), capabilities)
    }
```

在我們解說Code之前先看一張圖  
![Imgur](https://i.imgur.com/PDKe2Gs.png)  
是的這個function就是做測試環境設定
* MobileCapabilityType.PLATFORM_NAME: 測試平台，選擇Android
* MobileCapabilityType.DEVICE_NAME: 手機/模擬器名稱
* AndroidMobileCapabilityType.AUTO_GRANT_PERMISSIONS: 是否同意系統授權
* MobileCapabilityType.AUTOMATION_NAME: testing framework測試名稱
* MobileCapabilityType.APP: apk放置路徑
最後把設定資料傳給Appium Server(Server路徑可參考上圖上半部部分)  

我們需要每次測試前設定與測試完之後關閉
```kotlin

    lateinit var appDriver: AndroidDriver<MobileElement>
    
    @Before
    fun setUp() {
        appDriver = getAppiumDriver()
    }

    @After
    fun tearDown() {
        appDriver.quit()
    }
    
```

再來寫個簡單的測試碼

流程
1. 在Home頁點擊**換頁，不帶值**Button
2. 畫面顯示**Not Value**
```kotlin
    @Test
    fun testAppChangerPage() {
        with(appDriver) {
            manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS) //設定每個動作的最長等待時間

            findElementByXPath("${Utily.xPathName}android.view.View[3]/android.widget.Button").click()
            findElementByXPath("${Utily.xPathName}android.view.View[2]").also {
                assertEquals(it.text, "Not Value")
            }
        }
    }

```

利用findelementByXPath找相對應的元素(XPath可利用Appium Inspector找)，並做相對應的動作。
:::info
除了利用Xpath找以外也有找id、text等方式

因XPath很長所以前半部相同部分我寫在另一個檔案裡方便共用
:::

完整的Code
```kotlin

import io.appium.java_client.android.AndroidDriver
import io.appium.java_client.MobileElement
import io.appium.java_client.remote.AndroidMobileCapabilityType
import io.appium.java_client.remote.AutomationName
import io.appium.java_client.remote.MobileCapabilityType
import io.appium.java_client.remote.MobilePlatform
import org.junit.After
import org.junit.Assert.assertEquals
import org.junit.Before
import org.junit.Test
import org.openqa.selenium.remote.DesiredCapabilities
import java.net.URL
import java.util.concurrent.TimeUnit

class AppiumTest {

    lateinit var appDriver: AndroidDriver<MobileElement>

    fun getAppiumDriver(): AndroidDriver<MobileElement> {

        val capabilities = DesiredCapabilities().apply {
            setCapability(MobileCapabilityType.PLATFORM_NAME, MobilePlatform.ANDROID)
            setCapability(MobileCapabilityType.DEVICE_NAME, "Pixel 5 API 29")
            setCapability(AndroidMobileCapabilityType.AUTO_GRANT_PERMISSIONS, true)
            setCapability(MobileCapabilityType.AUTOMATION_NAME, AutomationName.ANDROID_UIAUTOMATOR2)
            setCapability(MobileCapabilityType.APP, "/Users/kannekichen/Desktop/app.apk")
        }
        return AndroidDriver(URL("http://127.0.0.1:4723/wd/hub"), capabilities)
    }

    @Before
    fun setUp() {
        appDriver = getAppiumDriver()
    }

    @After
    fun tearDown() {
        appDriver.quit()
    }

    @Test
    fun testAppChangerPage() {
        with(appDriver) {
            manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS) //設定每個動作的最長等待時間

            findElementByXPath("${Utily.xPathName}android.view.View[3]/android.widget.Button").click()
            findElementByXPath("${Utily.xPathName}android.view.View[2]").also {
                assertEquals(it.text, "Not Value")
            }
        }
    }
}
```

Utily
```kotlin

object Utily {

    val xPathName = "/hierarchy/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/" +
         "androidx.compose.ui.platform.ComposeView/android.view.View/android.view.View/android.view.View/"
}
```

測試結果:
![Imgur](https://i.imgur.com/CD6XNMq.png)