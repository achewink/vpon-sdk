---
layout:         "android"
title:          "Fundamental - Android Studio "
lead:           ""
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       android/fundamental/android-studio/
lang:            "en"
---

# VPON SDK 4 Fundamental
----
If you are using the previous version of vpon SDK, please read this first: [How to update to SDK4.2.x](../../../update-to-SDK4_2_x/)

1. Check your ad network from registering url first:<br>
Taiwan is <http://tw.pub.vpon.com/> <br>
China  is <http://cn.pub.vpon.com/>

2. If you register Taiwan platform, please use:
`vponBanner = new VpadnBanner(this, bannerId, VpadnAdSize.SMART_BANNER,
“TW”);`

3. If you register China platform, please use: <br>
`vponBanner = new VpadnBanner(this, bannerId, VpadnAdSize.SMART_BANNER,
“CN”);`
<br>

# Import SDK
---
To show Vpon banner on your Android App, you must complete three steps
below:  


1.  Import VPON SDK JAR into your Android Studio project.
2.  Declare com.vpadn.widget.VpadnActivity in AndroidManifest.xml.
3.  Set necessary permissions.


## Import SDK JAR
---
1. Find `libs` in your Android project (Route：Project Name -&gt; app
-&gt; libs)
![](../../../assets/img/ProjectLibFolder.jpg)


2. Right-click on `libs` and follow with a left-click on `Reveal in Finder`
![](../../../assets/img/DropJarFileToLibFolder.jpg)


3. Move the JAR downloaded to `libs` on finder (You can also grab Vpon JAR into `libs` on IDE)  
![](../../../assets/img/MainInterface.jpg)



4. Go back to your Android project and you will see that the Vpon JAR we just added shows up in [libs]. Make a right-click and choose `Add as library` to link reference. Please check the build.gradle at the same time to make sure there's a sentence " compile files('libs/vpon_SDK_version_name.jar') ". See the photo below.  
![](../../../assets/img/ModifyBuildGradle.jpg)



## VpadnActivity
---
Add com.vpadn.widget.VpadnActivity to your AndroidManifest.xml

``` java
      <activity
            android:name="com.vpadn.widget.VpadnActivity"
            android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
            android:theme="@android:style/Theme.Translucent"
            android:hardwareAccelerated="true" >
      </activity>
```
> **Note**: **EVERY** attribute is required!

<br>

## Permissions
---
Add following permissions in AndroidManifest.xml

```java
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```
The six permissions above are necessary. In addition, we recommend that you can add the following permission for being able to obtain more accurate banner related location.

```java
      <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```
Use following permission could make ads to be more accurate delivery,
and bring more revenue.

```java
      <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
```

Since there would be plenty of Video ads displayed on devices, we
recommend you to add hardware acceleration in your main Activity.

```xml
<activity
       android:name="com.vpadn.example.MainActivity"
       android:label="@string/app_name"
       android:configChanges="keyboardHidden|orientation"
       android:hardwareAccelerated="true" >
       <intent-filter>
           <action android:name="android.intent.action.MAIN" />
           <category android:name="android.intent.category.LAUNCHER" />
       </intent-filter>
   </activity>
```
  []: A-skd330-01.png "fig:A-skd330-01.png"
  [1]: A-sdk330-02.png "fig:A-sdk330-02.png"


# Coding for showing Banner
---
  Android apps are composed of View objects, Java instances the user sees as text areas, buttons and other controls. VpadnBanner is simply another View subclass displaying small HTML5 ads that respond to user touch.

  Like any view, an VpadnBanner may be created either purely in code or largely in XML.

  The five lines of code it takes to add a Vpon banner:

  1. Import `com.vpadn.ads.*`
  2. Declare an VpadnBanner instance
  3. Create it, specifying a unit ID—your VpadnBanner Banner ID
  4. Add the view to the UI
  5. Load it with an ad

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

# Create your banner in XML
---
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
              vpadn:bannerId= CHANGE ME
              vpadn:loadAdOnCreate="true"
              vpadn:platform="TW" />
      </RelativeLayout>
  </LinearLayout>
  </syntaxhighlight>
```
<br>
  As usual you must replace CHANGE ME with your Vpon Banner ID.
  You can use the following code to get the Test Banner If your banner ID has not been vetted.
<br>

```java
          VpadnAdRequest adRequest =  new VpadnAdRequest();
          HashSet<String> testDeviceImeiSet = new HashSet<String>();
          testDeviceImeiSet.add("your device advertising id"); //TODO: put Android device advertising id
          adRequest.setTestDevices(testDeviceImeiSet);
          vponBanner.loadAd(adRequest);
```
  You can get advertising ID by following methods:
  1. Search "advertising_id" from eclipse's log.
  2. Get your Advertising ID by clicking Ads in Google Settings from your phone directly.

# Download
---
[Go to download page](../../index.html#download)

# The Result
---
  When you now run your app you should see a banner at the top of the screen:
![](../../../assets/img/A-sdk330-03.png)
