---
layout:         "android"
title:          "基本使用 - Android Studio "
lead:           ""
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       /zh-tw/android/fundamental/android-studio/
lang:           "zh-tw"
---

# 撰寫 Banner
---
Android 應用程式由 View 物件所組成，也就是以文字區域和按鈕等控制項的形式向使用者呈現的 Java 執行個體。VpadnBanner 只是另一種 View 子類別，用來顯示由使用者點擊觸發的小型 HTML5 廣告。
和所有的 View 一樣，AdView 可以單用程式碼撰寫，也可以絕大部分用 XML 寫成。
加入橫幅廣告會用到程式碼：

1. 匯入 com.vpadn.ads.*
2. 宣告 VpadnBanner 執行個體
3. 建立例項，指定BannerId，也就是Vpon申請的BannerId
4. 將該檢視加進使用者介面
5. 透過廣告載入例項

最簡易的方式是在應用程式的 Activity 內進行上述所有步驟。

```java
  import com.vpadn.ads.*
  public class MainActivity extends Activity {
  	private RelativeLayout adBannerLayout;
  	private VpadnBanner vponBanner = null;
  	//TODO: VPON Banner ID
  	private String bannerId = CHANGE ME ;

         @Override
  	protected void onCreate(Bundle savedInstanceState) {
  		super.onCreate(savedInstanceState);
  		setContentView(R.layout.activity_main);
  		//get your layout view for Vpon banner
  		adBannerLayout = (RelativeLayout) findViewById(R.id.adLayout);
  		//create VpadnBanner instance
                  vponBanner = new VpadnBanner(this, bannerId, VpadnAdSize.SMART_BANNER, "TW");
  		VpadnAdRequest adRequest = new VpadnAdRequest();
  		//set auto refresh to get banner
  		adRequest.setEnableAutoRefresh(true);
                  //load vpon banner
  		vponBanner.loadAd(adRequest);
                  //add vpon banner to your layout view
  		adBannerLayout.addView(vponBanner);
  	}

  	@Override
  	protected void onDestroy() {
  		super.onDestroy();
  		if (vponBanner != null) {
  			//remember to call destroy method
  			vponBanner.destroy();
  			vponBanner = null;
  		}
  	}
    }
```
  <br>

# 使用 layout xml 設定 banner
---
也可以直接使用xml 定義Banner 這樣你就不需要寫任何java code

``` xml
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
              vpadn:bannerId= CHANGE_ME
              vpadn:loadAdOnCreate="true"
              vpadn:platform="TW" />
      </RelativeLayout>
  </LinearLayout>
```
<br>
記得將上面的 vpon:bannerId 填入你真實的 banner ID
如果你的 banner ID 還未經過審核可以使用下列的方式取得測試廣告
<br>

```java
      VpadnAdRequest adRequest =  new VpadnAdRequest();
      HashSet<String> testDeviceImeiSet = new HashSet<String>();
      testDeviceImeiSet.add("your device advertising id");
      //TODO: put Android device advertising id
      adRequest.setTestDevices(testDeviceImeiSet);
      vponBanner.loadAd(adRequest);
```
可以使用下列方式取得 device 上的 Advertising ID

1. 從 eclipse 上的 log 搜尋"advertising_id"
2. 直接操作手機: 設定 --> Google --> 廣告 --> 您的廣告 ID (Advertising ID)

# 其他訣竅
請參閱[中階使用](../advanced)中更多的橫幅廣告簡介。


# 下載 Sample code
---
[Go to download page]({{site.baseurl}}/zh-tw/index.html#download)

# 結果
---
現在只要執行這個應用程式，您應該就會在畫面上方看到橫幅廣告：
![gogo](../../../../assets/img/A-sdk330-03.png)
