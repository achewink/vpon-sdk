---
layout:         "default"
title:          "Web SDK"
lead:           "fantastic HTML5 ads you should not miss"
description:    "The description for this page in the meta data in header."
keywords:       "Keywords for this page, in the meta data"
permalink:       web/
lang:           "en"
---

#Overview
---
Vpon Mobile Web SDK enables mobile web developers to maximize their monetization on Android and iOS. <br>
<font color="red">
> **NOTE**：
> It ONLY supports ads on MOBILE SITES, and would not show any ad if you open your website on your personal computers.</font>
<br>


#Requirement
---
1. The basic concept of HTM.L <br>
2. Registering a banner ID for Vpon Mobile Web.<br>
3. Having the permission to modify code of mobile websites.
<br><br>

#Ad Formats
---
Vpon Mobile Web SDK supports the following formats:<br><br>

| Name              |    Size(WxH)  |
| :---------------- | :------------:|
| Banner            |    320x50     |  
| Medium Rectangle  |    300x250    |  


<br>
<br>

#Setups
---
##Basic Setup
1. You should insert the following snippet of code directly after the opening <body> tag on each page you want to load it:

```HTML
<body>
...
  <vpon vpon_ad_test="1"
        vpon_ad_licensy_key="your_first_vpon_banner_id_here"
        vpon_ad_format="320x50_mb"
        debug="true"></vpon>
...
  <vpon vpon_ad_test="1"
        vpon_ad_licensy_key="your_second_vpon_banner_id_here"
        vpon_ad_format="320x50_mb"
        debug="true"></vpon>
...
  <vpon vpon_ad_test="1"
        vpon_ad_licensy_key="your_third_vpon_banner_id_here"
        vpon_ad_format="300x250_mb"
        debug="true"></vpon>
...
  <script type="text/javascript"  src="http://m.vpon.com/sdk/vpadn-sdk.js"> </script>
</body>
```
> **Note:** <br>
>- You only allow to use 3 ads at most in one page and please use different banner ID for every ad.<br>
>- You only need to put <font color="red">just one</font> JavaScript before "</body>" like the sample code above. <br>
>- After saving the page, this code will load and initialize the SDK. You can load a test ad in the <vpon> tag. (If you want to see the official ad: vpon_ad_test="0")
<br>

##Advanced Setup
Name             |        Description                       | Necessary |  Example
:----------------------:| :-------------------------------:|:---:|:------------------------------------------------:
vpon\_ad\_licensy\_key| Banner ID                           |  Y   |<font color="red">Put your Vpon License Key</font>
vpon\_ad\_format      | Size：320x50\_mb, 300x250\_mb       |   Y |     “320x50\_mb”
vpon\_ad\_test        |   Test Ad                           | N   |   1(是)/0(否)，預設為(是)
debug                 | Debugging information in console訊  |  N   |   true/false，預設為false
openTab               |if open a new tab to show ad's contents  |N    |  true/false，預設為true
<br>
<br>

#Sample Code
---
```HTML
<html>
  <head><meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  </head>
  <body>
    <h1>The Test Page</h1>

    <div>
      <vpon vpon_ad_test="1"
            vpon_ad_licensy_key="Your Banner ID"
            vpon_ad_format="320x50_mb"
            debug="true"></vpon>
    </div>
    </br>
    <div>
      <vpon vpon_ad_test="1"
            vpon_ad_licensy_key="Your Banner ID"
            vpon_ad_format="300x250_mb"
            debug="true"></vpon>
    </div>
    <script type="text/javascript" src="http://m.vpon.com/sdk/vpadn-sdk.js"> </script>
  </body>
```

> **Note**:
> If you use iframe for embedding vpon's ad, please remember to modify the size of iframe to fit the right size of vpon's ad.


# FAQ
---
## Still can't see any ad
Please check the following items:

* Please open the page by mobile browser not the personal computer.<br>
* Clean the cache, delete cookie and reload the page.

## Still can't solve it
Open the debug mode and send all of  "Vpadn-" informations to [Vpon FAE]

[Vpon FAE]: mailto:fae@vpon.com