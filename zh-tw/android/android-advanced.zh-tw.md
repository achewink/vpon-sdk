---
layout:         "android"
title:          "Android - 進階設定"
lead:           "幫助您取得更多廣告功能與資料收集"
description:    ""
keywords:       "Keywords for this page, in the meta data"
permalink:       /zh-tw/android/advanced/
lang:            "zh-tw"
---

# VpadnAdRequest
  -----------------------------
  您可以先自訂 `VpadnAdRequest`，再將它傳送給 `VpadnBanner.loadAd`，讓 Vpon 以更精確的方式指定廣告 (com.adshow.ads.VpadnAdRequest)

## 指定接收廣告

  您可以使用這些屬性來指定要接收測試廣告的裝置或裝置 Set。若要確認 SDK 是否已順利整合，請加入您的測試裝置並執行應用程式，然後按一下所顯示的測試廣告。


```Java
  VpadnAdRequest request = new VpadnAdRequest();
  request.addTestDevice("your test device advertising id");
  //TODO 需要填入您測試機的advertising id
```

## 指定目標

您也可以指定位置和客層相關資訊。不過，為了保護使用者隱私，請只指定您的應用程式中現有的位置和客層資料。


```Java
VpadnAdRequest request = new VpadnAdRequest();
request.setGender(VpadnAdRequest.Gender.FEMALE);
request.setBirthday("1977-08-23");
```
  系統會以適當的方法取得使用者的位置


# VpadnAdListener
  ------------------------------

您可以選擇在傳送給 `VpadnBanner.setAdListener` 的物件中執行 `com.adshow.ads.VpadnAdListener`，藉此追蹤請求失敗或「點閱」等廣告生命週期事件。

```java
   public interface VpadnAdListener {
     void onVpadnReceiveAd(VpadnAd ad);
     void onVpadnFailedToReceiveAd(VpadnAd ad, VpadnAdRequest.VpadnErrorCode errorCode);
     void onVpadnPresentScreen(VpadnAd ad);
     void onVpadnDismissScreen(VpadnAd ad);
     void onVpadnLeaveApplication(VpadnAd ad);
   }
```

這個介面可由您的活動或任何其他物件執行：

```java
import com.vpadn.ads.*;
public class VpadnBannerExample extends Activity implements VpadnAdListener {
  //TODO: Implements all interface methods }
}
```

然後傳給 `VpadnBanner`：

```java
 vponBanner.setAdListener(this);
```

---
```java
  public void onVpadnReceiveAd(VpadnAd ad)
```
當 VpadnBanner.loadAd 成功時傳送。

```java
public void onFailedToReceiveAd(VpadnAd ad, VpadnAdRequest.VpadnErrorCode error)
```
當 loadAd 失敗時傳送；失敗原因通常是網路連線失敗、應用程式設定錯誤或廣告空間不足。

建議您將這些事件記錄下來以便偵錯：

```java
 @Override public void onFailedToReceiveAd(VpadnAd ad, VpadnAdRequest.VpadnErrorCode errorCode) { Log.d(MY_LOG_TAG, "failed to receive ad (" + errorCode + ")"); }
```

```java
public void onVpadnPresentScreen(VpadnAd ad)
```
當廣告因獲得使用者點擊，在您的應用程式之前建立了 Activity 並呈現出全螢幕廣告使用者介面時呼叫。

```java
public void onVpadnDismissScreen(VpadnAd ad)
```
當使用者關閉與 onVponPresentScreen 一同顯示的全螢幕 Activity，控制權也交還給應用程式時呼叫。

```java
public void onVpadnLeaveApplication(VpadnAd ad)
```
當 Ad 點擊會啟動新的應用程式時呼叫。




# Crazy Ad
---
會從 banner 自動展開成 Crazy Ad，全螢幕富媒體廣告的 Crazy Ad 呈現約 5~7 秒會自動關閉。
![海尼根廣告]


## 設定
---
在後台註冊申請流程中可選擇是否播放 Crazy Ad。<br>
進入 http://cn.adon.vpon.com/ 註冊中國區License Key。<br>
進入 http://tw.adon.vpon.com/ 註冊台灣區License Key。<br>
如圖:
![CrazyadSetting]


# Proguard Configuration
---
如果您的 App 本身需要經過 proguard 混淆，請增加下面的設定：<br>
-dontwarn c.\*\* <br>
-dontwarn com.vpon.\*\* <br>
-dontwarn vpadn.\*\* <br>
-keep class c.\*\*{ \*; } <br>
-keep class com.vpon.\*\* { \*; } <br>
-keep class vpon.\*\* { \*; } <br>
-keep class com.vpadn.\*\* { \*; } <br>
-keep class vpadn.\*\* { \*; } <br>


# Corona User
---
如果您 App 使用 Corona 欲串接 Vpon 廣告，我們建議您用 web SDK 的方式串接，使用方法如下:  

將 web SDK 裡的 html 寫進 local file 再讓 webview 去 load 這個 file (例如: webView:request( “localfile.html”, system.ResourceDirectory ))。  

HTML 內容可參考 Vpon wiki的web SDK 操作手冊: [Web SDK]  
更多 Corona SDK 文件可參考: [Corona Document]  





[海尼根廣告]:      {{site.imgurl}}/Crazyad.png
[CrazyadSetting]: {{site.imgurl}}/CrazyadSetting.png
[Web SDK]: {{site.baseurl}}/zh-tw/web/
[Corona Document]: http://docs.coronalabs.com/api/library/native/newWebView.html
