---
layout:         "android"
title:          "升级至 SDK 4.2.x "
lead:           ""
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       zh-cn/android/latest-news/update-to-SDK4_2_x/
lang:           "zh-cn"

---

# Steps to update
---
本文件是从SDK 4.0.0 或是SDK 4.1.0 升级到SDK 4.2.x的方法。因为新版SDK 4.2.x更改了package, class, interface和method的名称，另外删除 com.vpon.ads.VponPlatform这个class，请依照以下步骤做修改。

1.请将位于libs folder内旧的Vpon SDK jar档删除，并放入新的jar档 [SDK4.2.6]

2.更改import 的package, interface 和 class名称

```java
    com.vpon.ad.VponBanner -> com.vpadn.ad.VpadnBanner
    com.vpon.ad.VponAd -> com.vpadn.ad.VpadnAd
    com.vpon.ad.VponAdListener -> com.vpadn.ad.VpadnAdListener
    com.vpon.ad.VponAdRequest -> com.vpadn.ad.VpadnAdRequest
    com.vpon.ad.VponAdSize -> com.vpadn.ad.VpadnAdSize
    com.vpon.ad.VponInterstitialAd -> com.vpadn.ad.VpadnInterstitialAd
```

3.将VpadnBanner和VpadnInterstitialAd的constructor，最后一个参数VponPlatform.TW ，改为字串"TW"

由：

  `new VponBanner(this, bannerId1,VponAdSize.SMART_BANNER , VponPlatform.TW);`<br>
改为

  `new VpadnBanner(this, bannerId1,VpadnAdSize.SMART_BANNER ,"TW");`
<br>

4.改变Androidmanifest.xml 裡的activity tag，由

 ```xml
 <activity
      android:name="com.vpon.widget.VponActivity"
      android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
      android:theme="@android:style/Theme.Translucent"
      android:hardwareAccelerated="true">
</activity>
```
改为：

```xml
  <activity
      android:name="com.vpadn.widget.VpadnActivity"
      android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
      android:theme="@android:style/Theme.Translucent"
      android:hardwareAccelerated="true">
  </activity>
```

5.如果您有使用到 Interface VponAdListener 请改为 `VpadnAdListener` 这interface裡面所有的  method name 都由 vpon 改为 `vpadn`，如下：

`onVponReceiveAd` -> `onVpadnReceiveAd`  

`onVponFailedToReceiveAd` -> `onVpadnFailedToReceiveAd`  

`onVponPresentScreen` -> `onVpadnPresentScreen`  

`onVponDismissScreen` -> `onVpadnDismissScreen`  

`onVponLeaveApplication` -> `onVpadnLeaveApplication`

6. 如果有使用layout.xml 产生Vpon Banner，请将裡面所有 vpon 改为 `vpadn` 即可

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:vpadn="http://schemas.android.com/apk/lib/com.vpadn.ads"
    android:id="@+id/mainLayout"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical" >

<RelativeLayout
        android:id="@+id/adLayout"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content" >

        <com.vpadn.ads.VpadnBanner
            android:id="@+id/vpadnBannerXML"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            vpadn:adSize="SMART_BANNER"
            vpadn:autoFresh="true"
            vpadn:bannerId= CHANGE ME
            vpadn:loadAdOnCreate="true"
            vpadn:platform="TW" />
    </RelativeLayout>
</LinearLayout>

As usual you must replace CHANGE ME with your Vpon Banner ID.
You can use the following code to get the Test Banner If your banner ID has not been vetted

```java
      VpadnAdRequest adRequest =  new VpadnAdRequest();
      HashSet<String> testDeviceImeiSet = new HashSet<String>();
      testDeviceImeiSet.add("Advertising ID"); //TODO: put Android Advertising ID
      adRequest.setTestDevices(testDeviceImeiSet);
      vponBanner.loadAd(adRequest);
```

7. 如果有使用 Proguard 请将 vpon 改为 vpadn，改后范例:
-dontwarn c.**
-dontwarn com.vpon.**
-dontwarn vpadn.**
-keep class c.**{ *; }
-keep class com.vpon.** { *; }
-keep class vpon.** { *; }
-keep class com.vpadn.** { *; }
-keep class vpadn.** { *; }
