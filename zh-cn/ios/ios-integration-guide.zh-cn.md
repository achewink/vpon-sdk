---
layout: "ios"
title: "iOS - 串接说明"
lead: ""
description: 
keywords: 'Keywords for this page, in the meta data'
permalink: /zh-cn/ios/integration-guide/
lang: "zh-cn"
---
# Vpon SDK 基本使用
---
1. 请先从注册网址检查您的Ad Network平台<br>
Taiwan平台为: http://tw.pub.vpon.com/<br>
China平台为: http://cn.pub.vpon.com/<br>

2. 如果您申请的是Taiwan的平台，请使用:`vpadnAd.platform = @"TW"`;

3. 如果您申请的是China的平台，请使用:`vpadnAd.platform = @"CN"`;

4. 在 iOS8 之后如果没有看到 `didImpression`， 可能是因为 window 没有预设大小的关係，需要手动去setFrame设定大小，请注意！看到 `didImpression`的log才是正确的串接完成。

# 总览
---
若要在 iOS 应用程式中显示 Vpon 广告，只要在您的 Xcode 专案中导入 SDK，然后在使用者介面中加入相关指令就行了。

# 需求条件
---
VPON 广告 iOS 版的 SDK 需搭配 iOS 5.x 或更新版本 以及 XCode 4.4 或更新版本。

# 导入 SDK
---
解压缩后的 SDK 包含Objective-C 标头、一个执行期间程式库 要在应用程式中加入 Vpon 广告，您必须完成三个步骤：

1. 在专案中加入 `libAdOn.a`， `VpadnBanner.h` 与 `VpadnInterstitial.h`
2. 加入相关所需的 frameworks
3. 在 `Build Settings` 内 `Other Linker Flags` 请填入 `-all_load` 与 `-Obj-C`，并把 `Summary` 下把 `AdSupport` 设为 `Optional`
> **Note**: 上述三项缺一不可，请务必完成！

## 新增 SDK lib
1. 解压缩后的 SDK 包含一个 lib 档、及两个标头档。 对 Xcode 中的专案按一下滑鼠右键，然后选取 [Add Files to "Vpadn_BannerInter_x5"...] (在 "Vpadn_BannerInter_x5" 中新增档案)。
![IOS-add-file_vpadn.png]
2. 接着在 SDK 中选取 `libAdOn.a`, `VpadnBanner.h` 与 `VpadnInterstitial.h`
![IOS-add-lib&header_vpadn]
3. SDK lib 会参照 iOS 的 frameworks： <br  >
`AdSupport`, <br>
`AssetsLibrary`, <br>
`AudioToolbox`, <br>
`AVFoundation`, <br>
`CoreFoundation`, <br>
`CoreGraphics`, <br>
`CoreLocation`, <br>
`CoreMedia`, <br>
`CoreMotion`, <br>
`CoreTelephony`, <br>
`EventKit`, <br>
`Foundation`, <br>
`MediaPlayer`, <br>
`MessageUI`, <br>
`MobileCoreServices`, <br>
`QuartzCore`, <br>
`Security`, <br>
`StoreKit`, <br>
`SystemConfiguration`, <br>
`UIKit`

若要加入这些 Framework，请对 Vpadn_BannerInter_x5 这个专案名称按两下滑鼠，开启 `Build Phases` 分页下的 `Link Binary With Libraries` 下拉式选单，然后用画面上出现的 `+` 按钮加入 iOS SDK 中的架构。
![IOS-add-frameworks_vpadn]


# App Transport Security
---
iOS9 多了安全条款 App Transport Security (ATS)，若您使用 Xcode 7 建立 iOS9 专案，请参考[这篇]来修改部份设定

# 其他诀窍
请参阅[横幅广告](../banner)、[插页广告](../Interstitial)、[中介服务](../mediation)中获取更多简介。



[IOS-add-lib&header_vpadn]: {{site.imgurl}}/IOS-add-lib&header_vpadn.png
[IOS-add-file_vpadn.png]: {{site.imgurl}}/IOS-add-file_vpadn.png
[IOS-add-frameworks_vpadn]: {{site.imgurl}}/IOS-add-frameworks_vpadn.png
[这篇]: {{site.baseurl}}/zh-cn/ios/latest-news/ios9ats/
