---
layout:         "android"
title:          "升級至 SDK 4.2.x "
lead:           ""
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       zh-tw/android/latest-news/update-to-SDK4_2_x/
lang:           "zh-tw"

---

# Steps to update
---
本文件是從SDK 4.0.0 或是SDK 4.1.0 升級到SDK 4.2.x的方法。因為新版SDK 4.2.x更改了package, class, interface和method的名稱，另外刪除 com.vpon.ads.VponPlatform這個class，請依照以下步驟做修改。

1.請將位於libs folder內舊的Vpon SDK jar檔刪除，並放入新的jar檔 [SDK4.2.6]

2.更改import 的package, interface 和 class名稱

```java
    com.vpon.ad.VponBanner -> com.vpadn.ad.VpadnBanner
    com.vpon.ad.VponAd -> com.vpadn.ad.VpadnAd
    com.vpon.ad.VponAdListener -> com.vpadn.ad.VpadnAdListener
    com.vpon.ad.VponAdRequest -> com.vpadn.ad.VpadnAdRequest
    com.vpon.ad.VponAdSize -> com.vpadn.ad.VpadnAdSize
    com.vpon.ad.VponInterstitialAd -> com.vpadn.ad.VpadnInterstitialAd
```

3.將VpadnBanner和VpadnInterstitialAd的constructor，最後一個參數VponPlatform.TW ，改為字串"TW"

由：

  `new VponBanner(this, bannerId1,VponAdSize.SMART_BANNER , VponPlatform.TW);`<br>
改為

  `new VpadnBanner(this, bannerId1,VpadnAdSize.SMART_BANNER ,"TW");`
<br>

4.改變Androidmanifest.xml 裡的activity tag，由

 ```xml
 <activity
      android:name="com.vpon.widget.VponActivity"
      android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
      android:theme="@android:style/Theme.Translucent"
      android:hardwareAccelerated="true">
</activity>
```
改為：

```xml
  <activity
      android:name="com.vpadn.widget.VpadnActivity"
      android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
      android:theme="@android:style/Theme.Translucent"
      android:hardwareAccelerated="true">
  </activity>
```

5.如果您有使用到 Interface VponAdListener 請改為 `VpadnAdListener` 這interface裡面所有的  method name 都由 vpon 改為 `vpadn`，如下：

`onVponReceiveAd` -> `onVpadnReceiveAd`  

`onVponFailedToReceiveAd` -> `onVpadnFailedToReceiveAd`  

`onVponPresentScreen` -> `onVpadnPresentScreen`  

`onVponDismissScreen` -> `onVpadnDismissScreen`  

`onVponLeaveApplication` -> `onVpadnLeaveApplication`

6. 如果有使用layout.xml 產生Vpon Banner，請將裡面所有 vpon 改為 `vpadn` 即可

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

7. 如果有使用 Proguard 請將 vpon 改為 vpadn，改後範例:
-dontwarn c.**
-dontwarn com.vpon.**
-dontwarn vpadn.**
-keep class c.**{ *; }
-keep class com.vpon.** { *; }
-keep class vpon.** { *; }
-keep class com.vpadn.** { *; }
-keep class vpadn.** { *; }
