---
description: 带有唯一跟踪码的客户获取链接可以在 Adobe Mobile Services 中生成。当用户在单击生成的链接后从App Store下载并运行应用程序时，SDK会自动收集客户获取数据并将其发送到Adobe Mobile服务。
keywords: android；库；移动；sdk
seo-description: 带有唯一跟踪码的客户获取链接可以在 Adobe Mobile Services 中生成。当用户在单击生成的链接后从App Store下载并运行应用程序时，SDK会自动收集客户获取数据并将其发送到Adobe Mobile服务。
seo-title: 移动设备应用程序客户获取
solution: Marketing Cloud，Analytics
title: 移动设备应用程序客户获取
topic: 开发人员和实施
uuid: 4d32eae9-e856-4e40-8a29-2b5 bcc106 e0
translation-type: tm+mt
source-git-commit: 54150c39325070f37f8e1612204a745d81551ea7

---


# Mobile app acquisition {#mobile-app-acquisition}

带有唯一跟踪码的客户获取链接可以在 Adobe Mobile Services 中生成。当用户在单击生成的链接后从App Store下载并运行应用程序时，SDK会自动收集客户获取数据并将其发送到Adobe Mobile服务。

## 新的 Adobe Experience Cloud SDK 发行版本

查找与 Adobe Experience Platform Mobile SDK 相关的信息和文档？单击[此处](https://aep-sdks.gitbook.io/docs/)可获取最新的文档。

在 2018 年 9 月，我们发布了一个新的 SDK 主要版本。这些新的 Adobe Experience Platform Mobile SDK 可通过 [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 进行配置。

* 要开始配置，请转到 [Launch](https://launch.adobe.com/)。
* 要查看 Experience Platform SDK 存储库中的内容，请转到 [Github：Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks)。

>[!IMPORTANT]
>
> If you are using the Adobe Experience Platform Mobile SDKs with Adobe Launch, you **must** also install the Adobe Analytics Mobile Services extension to use Adobe Mobile Services features such as Acquisition links. 有关更多信息，请参阅 [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services)。For more information about using Acquisition and Marketing Links with the Experience Cloud SDKs, see [Acquisition and Marketing Links](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#acquisition-and-marketing-links).

>[!IMPORTANT]
>
>要使用 Acquisition，您&#x200B;**必须**&#x200B;具有 SDK 版本 4.1 或更高版本。

客户获取链接必须在 Adobe Mobile Services 中创建。有关更多信息，请参阅 [](/help/using/acquisition-main/acquisition-main.md)客户赢取。

**在 SDK 版本 4.13.1 及更高版本中**：

如果您无法使用在 Adobe Mobile Services 中创建的客户获取链接，仍然可以通过使用 Google Play Acquisition 由 SDK 收集并发送客户获取数据。

要从标准 Google Play Acquisition 促销活动中收集客户获取数据，请执行以下操作：

* 使用标准 Google Play 商店客户获取方法。

   自定义客户获取数据可用于标准 Google Play Acquisition 键值对。

* 在用户下载并运行从 Google Play 商店客户获取获得的应用程序时，将收集来自反向链接的数据并将这些数据发送至 Adobe Mobile Services。

   * The data is stored and available in the `AdobeDataCallback` instance that was registered earlier with the SDK.

      有关详细信息，请参阅 [配置方法](/help/android/configuration/methods.md)。

   * 使用或 `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL``MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` 事件类型。

   * Google Play 中的客户获取数据包含的自定义键将具有“`a.acquisition.custom.`”.”命名空间。

如果您使用在 Adobe Mobile Services 中创建的客户获取链接，请完成下列任务以将自定义数据添加到客户获取链接：

1. 为客户获取变量添加前缀“`adb`”。

   When the SDK receives the acquisition data from Adobe Mobile Services (on first launch), that data will be stored and also available in the `AdobeDataCallback` instance registered earlier with the SDK, as mentioned in [Configuration Methods](/help/android/configuration/methods.md).

1. 将使用或 `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL``MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` 事件类型。

1. 自定义数据密钥前缀为`a.acquisition.custom.`

>[!TIP]
>
>如果要向多个报表包发送数据，请使用应用程序中与报表包ID列表中第一个报表包关联的获取数据。

本节中的更新将使 SDK 能够通过客户获取链接发送客户获取数据。

## Tracking mobile acquisition {#section_CEA30C652AC8470784B8054E299B80FA}

1. 将库添加到项目中并实现生命周期。

   有关详细信息，请参阅 *在核心实施和生命周期* 中 [将SDK和Config文件添加到IntelliJ IDEA或Eclipse项目](/help/android/getting-started/dev-qs.md)。

1. 导入库：

   ```java
   import com.adobe.mobile.*;
   ```

1. 对反向链接实施 `BroadcastReceiver`：

   ```java
   package com.your.package.name;  // replace with your app package name 
   
   import android.content.BroadcastReceiver; 
   import android.content.Context; 
   import android.content.Intent; 
   
   public class GPBroadcastReceiver extends BroadcastReceiver { 
     @Override 
     public void onReceive(Context c, Intent i) { 
      com.adobe.mobile.Analytics.processReferrer(c, i); 
     } 
   }
   ```

1. 更新 `AndroidManifest.xml` 以启用在上一步骤中创建的 `BroadcastReceiver`：

   ```xml
   <receiver android:name="com.your.package.name.GPBroadcastReceiver" android:exported="true"> 
    <intent-filter> 
     <action android:name="com.android.vending.INSTALL_REFERRER" /> 
    </intent-filter> 
   </receiver>
   ```

1. Verify that the `ADBMobileConfig.json` file contains the required acquisition settings:

   ```xml
   "acquisition": { 
      "server": "c00.adobe.com", 
      "appid": "0652024f-adcd-49f9-9bd7-2552a4565d2f" 
   }, 
   "analytics": { 
     "referrerTimeout": 5, 
     ...
   ```

   >[!IMPORTANT]
   >
   >如果要向多个报表包发送数据，请使用应用程序中与报表包ID列表中第一个报告套件关联的获取设置(获取服务器和appid)。

   `acquisition` 设置由 Adobe Mobile Services 生成，不应对其进行更改。For more information about how to download a customized `ADBMobileConfig.json` file with the `acquisition` settings pre-configured, see [Before You Start](/help/android/getting-started/requirements.md).

启用这些设置后，将会在首次启动应用程序后的初始生命周期调用中自动发送客户获取数据。

>[!CAUTION]
>
>`referrerTimeout` 必须设置为大于的值才能启用应用程序获取。