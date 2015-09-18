---
layout:         "android"
title:          "Android - Admob 使用串接"
lead:           ""
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       /zh-tw/android/mediation/admob/
lang:           "zh-tw"
---

# Google AdMob mediation
--------
google AdMob mediation 請看[這裡]

# Admob Mediation 操作圖示
-----

1. 請登入到 [這裡][]  
![1]  

2. 盈利 -&gt; 透過新應用程式盈利  
![][2]  

3. 選取應用程式:
  (1) 填入app name
  (2) 選取平台
  (3) 點選 “新增應用程式"
![][3]  

4. 選取廣告格式並對廣告單元命名: (1) 選擇橫幅廣告或者插頁廣告 (2) 設定,  (3) 廣告單元名稱(ex. Vpon\_Banner)  (4) 儲存  
![][4]  

5. 得到一組廣告單元編號，選取完成  
![][5]  

6. 編輯中介服務  
![][6]  

7. 新增廣告連播網  
![][7]  

8. 設定Vpon進入您的聚合列表：  
(1) 在可用的廣告聯播網中找到 Vpon  
(2) Vpon Ad Id: 填入您在 Vpon 後台申請的版位ID  
(3) Zone: 選擇您欲請求的廣告平台的地區  
(例：如果您的 App 是欲給大陸平台使用者使用，則您需在此欄位中填入`cn`，若您 app 是給除了大陸平台以外地區使用者使用則填入`tw`)  

![][8]  


# 串接 Vpon 進專案
您需將載入兩個 Jar 檔進入您專案中的 libs 資料夾，分別是：admob-adapter-\*\*\*\*.jar 和 vpadn-sdk-\*\*\*-\*\*\*-\*\*\*.jar.  
![][9]  



# 需求條件
-----
1. 請確認您已安裝最新版的[Android SDK]，並至少在 Android v3.2 (target in project.properties to android-13)下編譯。  
2. Google Mobile Ads SDK可在Android 2.3以上的版本(在 AndroidManifest.xml 設定 android:minSdkVersion 為至少 9)執行。  

# 導入SDK
---
以下的步驟為將Google Mobile Ads SDK 導入您的App中:  

1. 新增並 reference Google Play Services library到您的 Eclipse/Android Studio workspace.  
2. 在 AndroidManifest.xml中新增 meta-data tag.  
3. 在 AndroidManifest 中宣告 com.google.android.gms.ads.AdActivity.  
4. 在 manifest 中加入 permissions  

## Google Play Services library
請先安裝設定 Google Play Service SDK: [Android instructions]

### Eclipse
---
a.在您的應用程式專案中按右鍵並選擇“內容”  

![][10]  

b.選擇Android -&gt;
Add...尋找google-play-services\_lib內容後按下OK新增Google Play services
library.  

![][11]  

如圖示，您的專案已經reference Google Play services library.  

![][12]  

### Android Studio
---
1. 請打開 `app` 模組下的 `build.gradle`
> **Note**: Android Studio 專案下有兩個 `build.gradle`，請小心以免搞混

2. 增加 build rule 在 dependencies 底下，已取得最新版 `play-services`

```groovy
apply plugin: 'com.android.application'
    ...

    dependencies {
      compile 'com.google.android.gms:play-services:+'
    }
```
接著，存擋並至 toolbar 點選 **Sync Project with Gradle Files**

## 新增 meta-data tag
Google Play Service需要在AndroidManifest.xml中加入以下設定:  

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.company"
          android:versionCode="1" android:versionName="1.0">  
 <application android:icon="@drawable/icon" android:label="@string/app_name"
               android:debuggable="true">  
  <span style="color:#ff0000"><meta-data android:name="com.google.android.gms.version"
             android:value="@integer/google_play_services_version"/></span>  
   <activity android:label="@string/app_name" android:name="BannerExample">  
     <intent-filter>  
       <action android:name="android.intent.action.MAIN"/>  
       <category android:name="android.intent.category.LAUNCHER"/>  
     </intent-filter>  
   </activity>  
 </application>  
</manifest>
```

## 宣告 AdActivity
---
Mobile Ads SDK 需要在AndroidManifest.xml中宣告com.google.android.gms.ads.AdActivity  

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.company"
          android:versionCode="1" android:versionName="1.0">  
 <application android:icon="@drawable/icon" android:label="@string/app_name"
               android:debuggable="true">  
   <meta-data android:name="com.google.android.gms.version"
               android:value="@integer/google_play_services_version"/>  
   <activity android:label="@string/app_name" android:name="BannerExample">  
     <intent-filter>  
       <action android:name="android.intent.action.MAIN"/>  
       <category android:name="android.intent.category.LAUNCHER"/>  
     </intent-filter>  
   </activity>  
   <span style="color:#ff0000">
     <activity android:name="om.google.android.gms.ads.AdActivity"
       android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"/></span>
 </application>
</manifest>
```
## Permissions
---
加入以下permission 在您的AndroidManifest.xml<br>
`'INTERNET"` 此為必要，以開啓網路功能進行傳輸。<br>
`'ACCESS_NETWORK_STATE"` 此為選擇，用來讀取使用者當前的網路狀態。<br>

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.company"
          android:versionCode="1" android:versionName="1.0">
  <application android:icon="@drawable/icon" android:label="@string/app_name"
               android:debuggable="true">
    <meta-data android:name="com.google.android.gms.version"
               android:value="@integer/google_play_services_version"/>
    <activity android:label="@string/app_name" android:name="BannerExample">
      <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
      </intent-filter>
    </activity>
    <activity android:name="com.google.android.gms.ads.AdActivity"
              android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"/>
  </application>
  <span style="color:#ff0000"><uses-permission android:name="android.permission.INTERNET"/>
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/></span>
 </manifest>
```

# Banner 橫幅廣告
---
要在您的Android app中展示橫幅廣告，只需要簡單的新增 com.google.android.gms.ads.AdView 到您的使用者介面。
新增 com.google.android.gms.ads.AdView

利用以下五個步驟新增出一個橫幅廣告:
• 匯入 com.google.android.gms.ads.*
• 宣告一個 AdView物件
• 建立並指定一個 ad unit ID
• 在使用者介面中新增 view
• 取得banner

最簡易的方法為在您的Activity中做出所有的步驟.

```Java
  import com.google.android.gms.ads.*;

  public class BannerExample extends Activity {
  private AdView adView;

  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    // Create the adView.
    adView = new AdView(this);
    adView.setAdUnitId(MY_AD_UNIT_ID);
    adView.setAdSize(AdSize.BANNER);

    // Lookup your LinearLayout assuming it's been given
    // the attribute android:id="@+id/mainLayout".
    LinearLayout layout = (LinearLayout)findViewById(R.id.mainLayout);

    // Add the adView to it.
    layout.addView(adView);

    // Initiate a generic request.
    AdRequest adRequest = new AdRequest.Builder().build();

    // Load the adView with the ad request.
    adView.loadAd(adRequest);
  }

  @Override
  public void onPause() {
    adView.pause();
    super.onPause();
  }

  @Override
  public void onResume() {
    super.onResume();
    adView.resume();
  }

  @Override
  public void onDestroy() {
    adView.destroy();
    super.onDestroy();
   }
 }
```
參考更多的 banner 設定: [here][13]


# Interstitial 插頁廣告
---
和AdView的使用方式相似:
• 匯入 `com.google.android.gms.ads.*`
• 宣告物件
• 建立並指定一個和banner不同的 AdMob Ad Unit ID。

同樣的，最方便的方式為在您的 Activity 中做以下的步驟。

```Java
 import com.google.android.gms.ads.*;
 public class BannerExample extends Activity {

  private InterstitialAd interstitial;

  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    // Create the interstitial.
    interstitial = new InterstitialAd(this);
    interstitial.setAdUnitId(MY_AD_UNIT_ID);

    // Create ad request.
    AdRequest adRequest = new AdRequest.Builder().build();

    // Begin loading your interstitial.
    interstitial.loadAd(adRequest);

  }

  // Invoke displayInterstitial() when you are ready to display an interstitial.
  public void displayInterstitial() {
    if (interstitial.isLoaded()) {
      interstitial.show();
     }
   }
 }
```

# 下載 Sample Code
--------------------
[Download Sample Code]

  [這裡]: https://developers.google.com/mobile-ads-sdk/docs/admob/mediation#android
  []: http://www.google.com.tw/ads/admob/
  [1]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid1.png
  [2]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid2.png
  [3]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid3.png
  [4]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid4.png
  [5]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid5.png
  [6]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid6.png
  [7]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid7.png
  [8]:  {{site.baseurl}}/assets/img/AdMobScreenshotTradChineseAndroid8.png
  [9]:  {{site.baseurl}}/assets/img/AdMobLibJarFiles.jpg
  [10]: {{site.baseurl}}/assets/img/GooglePlay_Properties.png
  [11]: {{site.baseurl}}/assets/img/GooglePlay_Addlib.png
  [12]: {{site.baseurl}}/assets/img/GooglePlay_Addlib2.png
  [Download Sample Code]: {{site.baseurl}}/zh-tw/android/download/#admob
  [Android SDK]: https://developer.android.com/sdk/index.html
  [Android instructions]: https://developer.android.com/google/play-services/setup.html
  [13]: https://developers.google.com/mobile-ads-sdk/docs/admob/intermediate#play
