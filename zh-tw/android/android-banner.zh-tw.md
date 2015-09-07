---
layout:         "android"
title:          "Android SDK 中級使用"
lead:           "Banner Ad"
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       /zh-tw/android/advanced/
lang:           "zh-tw"
---
# 橫幅廣告大小
---
除了支援手機上的 320x50 大小外，VPON還支援各種不同的橫幅廣告：

大小 (寬度x高度)             |     說明       |  VponAdSize 常數值
:------------------------: | :-------------:| :-----------------------------:
320x50                     | 標準橫幅廣告     | VpadnAdSize.BANNER
468x60                     | IAB 全橫幅廣告   | VpadnAdSize.IAB\_BANNER
728x90                     | IAB 超級橫幅廣告 |  VpadnAdSize.IAB\_LEADERBOARD
device width x auto height | Smart Banner    |  VpadnAdSize.SMART\_BANNER

如無特定需求，我們建議您直接使用上面最後一項smart banner即可 (目前不支援VpadnAdSize.IAB\_WIDE\_SKYSCRAPER)


#  更新廣告
  --------

  如果您在伺服器的 VPON 帳戶中指定了更新速率，且需要使用下面的sample才會啟動banner自動更新

```java
 VpadnAdRequest adRequest = new VpadnAdRequest();
 //設定成true才會自動更新 adRequest.setEnableAutoRefresh(true);
 adShowBanner.loadAd(adRequest);
```


# com.adshow.ads.VpadnAdRequest
  -----------------------------
  您可以先自訂 VpadnAdRequest，再將它傳送給 VpadnBanner.loadAd，讓 VPON 以更精確的方式指定廣告。

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


  系統會以[適當的方法][1]取得使用者的[位置][2]。

# com.adshow.ads.VpadnAdListener
  ------------------------------

您可以選擇在傳送給 VpadnBanner.setAdListener 的物件中執行 com.adshow.ads.VpadnAdListener，藉此追蹤請求失敗或「點閱」等廣告生命週期事件。

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

然後傳給 VpadnBanner：

```java
 vponBanner.setAdListener(this);
```

  public void onVpadnReceiveAd(VpadnAd ad) 當 VpadnBanner.loadAd 成功時傳送。 public void onFailedToReceiveAd(VpadnAd ad, VpadnAdRequest.VpadnErrorCode error) 當 loadAd 失敗時傳送；失敗原因通常是網路連線失敗、應用程式設定錯誤或廣告空間不足。建議您將這些事件記錄下來以便偵錯：

```java
 @Override public void onFailedToReceiveAd(VpadnAd ad, VpadnAdRequest.VpadnErrorCode errorCode) { Log.d(MY\_LOG\_TAG, "failed to receive ad (" + errorCode + ")"); }
```

  public void onVpadnPresentScreen(VpadnAd ad) 當廣告因獲得使用者點擊，在您的應用程式之前建立了 Activity 並呈現出全螢幕廣告使用者介面時呼叫。 public void onVpadnDismissScreen(VpadnAd ad) 當使用者關閉與 onVponPresentScreen 一同顯示的全螢幕 Activity，控制權也交還給應用程式時呼叫。 public void onVpadnLeaveApplication(VpadnAd ad) 當 Ad 點擊會啟動新的應用程式時呼叫。


# 其他訣竅
  ----
  請參閱[進階指南][3]中有關插頁式廣告的簡介。


# Download Sample Code
  -------------------
  SDK 4 JAR 檔 在Sample code libs folder內

  [Go to download page](/tw/#download)


[1]: http://developer.android.com/guide/topics/location/strategies.html
[2]: http://developer.android.com/reference/android/location/Location.html
[3]: interstitial-ad/
