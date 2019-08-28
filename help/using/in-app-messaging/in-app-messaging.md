---
description: 创建、管理和报告应用程序内消息和推送消息。
keywords: mobile
seo-description: 创建、管理和报告应用程序内消息和推送消息。
seo-title: 消息传送
solution: Marketing Cloud，Analytics
title: 消息传送
topic: 量度
uuid: e32d3e35-2d09-4df-8919-75dc895abcb3
translation-type: tm+mt
source-git-commit: 3b744229b3fc288363be74c3c4adcd71ecc4fad4

---


# 消息传送 {#messaging}

您可以创建、管理和报告应用程序内和推送消息。

## 新的 Adobe Experience Cloud SDK 发行版本

查找与 Adobe Experience Platform Mobile SDK 相关的信息和文档？单击[此处](https://aep-sdks.gitbook.io/docs/)可获取最新的文档。

在 2018 年 9 月，我们发布了一个新的 SDK 主要版本。这些新的 Adobe Experience Platform Mobile SDK 可通过 [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 进行配置。

* 要开始配置，请转到 [Launch](https://launch.adobe.com/)。
* 要查看 Experience Platform SDK 存储库中的内容，请转到 [Github：Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks)。

>[!IMPORTANT]
>
> If you are using the Adobe Experience Platform Mobile SDKs with Adobe Launch, you **must** also install the Adobe Analytics Mobile Services extension to use Adobe Mobile Services features such as Acquisition links. 有关更多信息，请参阅 [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services)。有关在 Experience Platform SDK 中使用推送消息和应用程序内消息传送的信息，请参阅[设置推送消息](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-messaging)和[设置应用程序内消息传送](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-in-app-messaging)。

## In-app messages {#section_8984F4568BC24D32A87429FFCB5184A6}

应用程序内消息会根据用户的操作和特征，实时提供给用户。消息会从 SDK 已跟踪的 Analytics 数据触发。

支持以下消息类型：

* 自定义消息和具有特定主题的消息
* 全屏消息
* 本机警报消息
* 本地通知消息

为了帮助您了解应用程序内消息传递的工作原理，以下是一些附加信息：

* 应用程序内消息需要SDK4.2或更高版本。
* 您必须指定具有移动应用程序管理员权限的用户。

   这些权限允许访问客户获取链接和应用程序内消息。有关详细信息，请参阅 [角色和权限](/help/using/gs/c-mob-roles-and-permissions.md)。
* 在消息获得批准后，便会自动将消息发布到应用程序。
* 如果消息参数（例如特征、触发器和时间安排）满足相应要求，则 SDK 会向用户呈现消息。
* 消息可以包含使用在线 URL 的自定义 HTML 或图像。

   还可指定应用程序包中的备份图像或备用图像，以供离线状态下触发的消息使用。
* 消息激活并完成后会提供总查看次数、点进率等报表。
* 有些模板可用于自定义消息，您可以使用这些模板轻松地创建自己的应用程序内消息。

## Push messages {#section_90555A55BCE7427A90B1577E14BEF51B}

推送消息将发送给选择接收通知的用户。您可以将这些推送消息定位到 Analytics 区段或自定义区段中的用户。推送消息可以在应用程序之外的其他许多地方显示，因此可用于重新吸引消极用户或传达特定于时间的和位置的信息。

配置推送消息之前，请参阅 [入门项目以启用推送消息](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md)。在执行这些任务之后，您必须在应用程序的设置中配置推送消息。有关详细信息，请参阅[配置推送消息](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-push-messaging.md)。