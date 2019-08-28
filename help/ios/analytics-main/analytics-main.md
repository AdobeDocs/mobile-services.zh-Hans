---
description: 此信息可帮助您将 iOS SDK 与 Adobe Analytics 结合使用。
seo-description: 此信息可帮助您将 iOS SDK 与 Adobe Analytics 结合使用。
seo-title: 分析概述
solution: Marketing Cloud，Analytics
title: 分析概述
topic: 开发人员和实施
uuid: 8c7fb76a-be0 b-4465-8151-eg7 bug11 b55
translation-type: tm+mt
source-git-commit: 9257d6b6c2c14d0422cda65fcc9c677ac5ac47a9

---


# 分析概述 {#analytics}

本部分中的信息可帮助您将iOS SDK与Adobe Analytics一起使用。

## 新的 Adobe Experience Cloud SDK 发行版本

查找与 Adobe Experience Platform Mobile SDK 相关的信息和文档？单击[此处](https://aep-sdks.gitbook.io/docs/)可获取最新的文档。

在 2018 年 9 月，我们发布了一个新的 SDK 主要版本。这些新的 Adobe Experience Platform Mobile SDK 可通过 [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 进行配置。

* 要开始配置，请转到 Launch。
* 要查看 Experience Platform SDK 存储库中的内容，请转到 [Github：Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks)。

>[!IMPORTANT]
>
> If you are using the Adobe Experience Platform Mobile SDKs with Adobe Launch, you **must** also install the Adobe Analytics Mobile Services extension to use Adobe Mobile Services features such as in-App messaging, push notifications or Acquisition links. 有关更多信息，请参阅 [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services)。

## 生成Analytics跟踪标识符

在 SDK 中，标识符用于跟踪用户，标识符的层次结构如下：

1. 自定义访客标识符 (VID)
2. Analytics 跟踪标识符 (AID)
3. Experience Cloud 标识符 (MID)

>[!TIP]
>
>Experience Cloud标识符的正确缩写为EID。尽管 SDK 仍然使用 MID，但它用的是旧名称。AID 有时候也被称为“跟踪标识符”，当应用程序未配置为使用 MID 时，SDK 会生成 AID。在应用程序启动和升级过程中，该值会保留在 `NSUserDefaults` 中。如果用户从其设备中删除应用程序，然后重新安装该应用程序，或者如果应用程序开发人员清除 `NSUserDefaults`，则 SDK 会生成一个新的标识符。这个流程会在 Analytics 报表中生成新用户。

对于引入身份服务支持 (MID) 的应用程序中的用户而言，现有 AID 值会随 Analytics 点击一起发送，并且 Analytics 点击包含 AID 和 MID。对于提供身份服务支持的应用程序中的新用户而言，Analytics 请求仅包含 MID。For more information about identifying visitors, see [Identify visitors](https://docs.adobe.com/content/help/en/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-visid.html).