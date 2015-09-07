---
layout:         "default"
title:          "Update to SDK 4.2.x "
lead:           "sub-title"
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:      update-to-SDK4_2_x/
lang:            "en"
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
3.You have to modify the last one parameter of the constructor of VpadnBanner and VpadnInterstitialAd. Please change the VponPlatform.TW to be the String “TW” or “CN”(only for China) original version：  

    `new VponBanner(this, bannerId1,VponAdSize.SMART_BANNER , VponPlatform.TW);`

    Change it like this:

    `new VpadnBanner(this, bannerId1,VpadnAdSize.SMART_BANNER ,"TW");`

4.Please change activity tag in Androidmanifest.xml:  <br>
original version:

 ```xml
 <activity
            android:name="com.vpon.widget.VponActivity"
            android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
            android:theme="@android:style/Theme.Translucent"
            android:hardwareAccelerated="true"
            >
           </activity>
```
Change it like this:

```xml
        <activity
            android:name="com.vpadn.widget.VpadnActivity"
            android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
            android:theme="@android:style/Theme.Translucent"
            android:hardwareAccelerated="true"
            >  
        </activity>
```

5.If you used the interface of VponAdListener, please modify it to
VpadnAdListener.  
All names of methods used in interface should be changed to vpadn, for
example:  

`onVponReceiveAd` -> `onVpadnReceiveAd`  

`onVponFailedToReceiveAd` -> `onVpadnFailedToReceiveAd`  

`onVponPresentScreen` -> `onVpadnPresentScreen`  

`onVponDismissScreen` -> `onVpadnDismissScreen`  

`onVponLeaveApplication` -> `onVpadnLeaveApplication`

  [SDK4.2.6]: http://m.vpon.com/sdk/vpadn-sdk-obf426-8270410.jar
