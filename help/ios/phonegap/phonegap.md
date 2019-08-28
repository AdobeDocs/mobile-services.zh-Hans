---
description: 使用该插件，您可以从 PhoneGap 项目发送 iOS AppMeasurement 调用。
keywords: PhoneGap
seo-description: 使用该插件，您可以从 PhoneGap 项目发送 iOS AppMeasurement 调用。
seo-title: PhoneGap 插件
solution: Marketing Cloud，Analytics
title: PhoneGap 插件
topic: 开发人员和实施
uuid: f88bcf10-1f9e-4c97-b348-40db797 c9923
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# PhoneGap plug-in{#phonegap-plug-in}

使用该插件，您可以从 PhoneGap 项目发送 iOS AppMeasurement 调用。

## 新的 Adobe Experience Cloud SDK 发行版本

查找与 Adobe Experience Platform Mobile SDK 相关的信息和文档？单击[此处](https://aep-sdks.gitbook.io/docs/)可获取最新的文档。

在 2018 年 9 月，我们发布了一个新的 SDK 主要版本。这些新的 Adobe Experience Platform Mobile SDK 可通过 [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 进行配置。

* 要开始配置，请转到 Launch。
* 要查看 Experience Platform SDK 存储库中的内容，请转到 [Github：Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks)。

>[!IMPORTANT]
>
> If you are using the Adobe Experience Platform Mobile SDKs with Adobe Launch, you **must** also install the Adobe Analytics Mobile Services extension to use Adobe Mobile Services features such as in-App messaging, push notifications or Acquisition links. 有关更多信息，请参阅 [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services)。

要创建PhoneGap项目，请参阅 [PhoneGap](https://helpx.adobe.com/experience-manager/6-4/mobile/using/phonegap.html)。

## 使用 npm 安装插件: {#section_43229E57C16944C0B51531CB92089189}

1. 运行以下命令：

   ```
   cordova plugin add adobe-mobile-services
   ```

## 手动安装插件 {#section_D53BA60D488C4DB8AD2BDF90439C180A}

### 包括AppMeasurement库

要包含 AppMeasurement，请执行以下操作：

1. Drag `ADBMobile_PhoneGap.h` and  `ADBMobile_PhoneGap.m` into the **[!UICONTROL Plugins]** folder in your Xcode project.
1. 完成以下设置：

   1. Select **[!UICONTROL Copy items into destination group's folder (if needed)]**.
   1. 选择您要使用 AppMeasurement 代码的目标位置。

1. Drag `ADB_Helper.js` into the `www` folder in your project.
1. `res/xml` 在文件夹中，通过添加以下内容打开 `config.xml` 和注册新插件：

   ```
   <feature name="ADBMobile_PhoneGap"> 
     <param name="ios-package" value="ADBMobile_PhoneGap" /> 
   </feature>
   ```

### 添加应用程序权限

AppMeasurement 库需要执行以下操作：

1. 启动 Xcode IDE 并打开您的应用程序。
1. 将 **[!UICONTROL AdobeMobile]文件夹拖到您的 Xcode 项目中，并完成以下设置：**

   1. Select **[!UICONTROL Copy items into destination group's folder (if needed)]**.
   1. Select **[!UICONTROL Create groups for any added folders]**.
   1. Select the targets where you want to use AppMeasurement code and click **[!UICONTROL Finish]**.
   ![](assets/xcode-settings.png){width=“672”}

1. 在您的项目目标的&#x200B;**[!UICONTROL 生成阶段]**&#x200B;选项卡中，展开&#x200B;**将二进制文件与库关联]部分，然后添加以下库：[!UICONTROL **

   * `libsqlite3.dylib`
   * `SystemConfiguration.framework`

1. 确认您的应用程序在生成时没有出现意外错误。

## Implement custom tracking {#section_FD102B3CDAA4492FB04E56BF17E28663}

In `html` files where you want to use tracking, add the following to the `<head>` tag:

```html
<script type="text/javascript" charset="utf-8" src="ADB_Helper.js"></script>
```
