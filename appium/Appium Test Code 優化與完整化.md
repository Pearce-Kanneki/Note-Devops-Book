---
title: Appium Test Code 優化與完整化
tags: test
---

# Appium Test Code 優化與完整化

在上一篇中我們寫了一簡單的Test Code，但是裡面有部分程式碼會在寫其他Test Code重複出現，所以筆者把重複的Code提出來方便其他Test Case可以繼承而不用重複寫，成果如下

BaseTest.kt

```kotlin
package appium

import Utily
import io.appium.java_client.MobileElement
import io.appium.java_client.android.AndroidDriver
import io.appium.java_client.remote.AndroidMobileCapabilityType
import io.appium.java_client.remote.AutomationName
import io.appium.java_client.remote.MobileCapabilityType
import io.appium.java_client.remote.MobilePlatform
import org.junit.After
import org.junit.Before
import org.openqa.selenium.remote.DesiredCapabilities
import java.net.URL
import java.util.concurrent.TimeUnit

open class BaseTest {

    lateinit var appDriver: AndroidDriver<MobileElement>

    private fun getAppiumDriver(): AndroidDriver<MobileElement> {
        with(DesiredCapabilities()) {

            setCapability(MobileCapabilityType.PLATFORM_NAME, MobilePlatform.ANDROID)
            setCapability(MobileCapabilityType.DEVICE_NAME, Utily.DEVICE_NAME)
            setCapability(AndroidMobileCapabilityType.AUTO_GRANT_PERMISSIONS, true)
            setCapability(MobileCapabilityType.AUTOMATION_NAME, AutomationName.ANDROID_UIAUTOMATOR2)
            setCapability(MobileCapabilityType.APP, Utily.APK_PATH)

            return AndroidDriver(URL(Utily.APPIUM_URL), this)
        }
    }

    @Before
    fun setUp() {
        appDriver = getAppiumDriver()
        appDriver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS) //設定每個動作的最長等待時間
    }

    @After
    fun tearDown() {
        appDriver.quit()
    }
}
```

Utily.kt

```kotlin
object Utily {

    const val xPathName = "/hierarchy/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/" +
         "androidx.compose.ui.platform.ComposeView/android.view.View/android.view.View/android.view.View/"

    const val DEVICE_NAME = "Pixel 5 API 29"
    const val APK_PATH = "/Users/kannekichen/Desktop/app.apk"
    const val APPIUM_URL = "http://127.0.0.1:4723/wd/hub"
}
```

之後要改測試機、APK位置或Appium Server位置只要到Utily改就能一次改全部了。\
然後再把上一篇Test Code獨立出來，如下

```kotlin
package appium

import Utily
import org.junit.Assert
import org.junit.Test

class HomeTest: BaseTest() {

    @Test
    fun clickNotValueButton_changerPage_returnNotValue() {
        with(appDriver) {

            findElementByXPath("${Utily.xPathName}android.view.View[3]/android.widget.Button").click()
            findElementByXPath("${Utily.xPathName}android.view.View[2]").also {
                Assert.assertEquals(it.text, "Not Value")
            }
        }
    }
}
```

最後再把其他頁面的Test Case完成 完整Code GitHub連結: [Appium Test Code](https://github.com/Pearce-Kanneki/Appium-Android-test)

其他參考: [Appium 常用API](https://www.cnblogs.com/juno3550/p/15505480.html)
