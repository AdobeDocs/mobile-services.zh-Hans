---
description: 此信息可帮助您排查推送消息问题。
keywords: mobile
seo-description: 此信息可帮助您排查推送消息问题。
seo-title: 推送消息故障诊断
solution: Marketing Cloud，Analytics
title: 推送消息故障诊断
topic: 量度
uuid: c4a9371-6691-4a2c-a6 c1 c1-b9 f901 a41599
translation-type: tm+mt
source-git-commit: 12e01e112debffd877dd62f1fd2505724b2aae7d

---


# 推送消息故障诊断 {#troubleshooting-push-messaging}

此信息可帮助您排查推送消息问题。

## 为什么发送推送消息有时会出现延迟？

以下延迟类型可能与 Mobile Services 的推送消息有关。

* 等待 Analytics 点击

   每个报表包都有一个设置来确定何时处理传入的 Analytics 点击。默认为小时，即 1 小时。对 Analytics 点击的实际处理可能最多需要 30 分钟，但通常为 15 到 20 分钟。例如，一个报表包每小时处理一次点击。如果将最多 30 分钟的处理时间包括在内，那么一个传入点击可能最多需要 90 分钟才可用于推送消息。如果用户在上午 9:01 启动应用程序，则该点击将在上午 10:15 到 10:30 期间在 Mobile Services 用户界面中显示为新的独特用户。

* 等待推送服务

   推送服务(APNS或FCM)可能不会立即发送消息。偶尔会有 5 到 10 分钟的延迟。在消息页面上，您可以单击消息的&#x200B;**查看**&#x200B;链接来验证推送消息是否已发送到推送服务。在报表中，成功发送到推送服务的消息数会列在&#x200B;**[!UICONTROL 已发布]列中。**

   >[!TIP]
   >
   >推送服务不保证发送消息。

   有关服务可靠性的更多信息，请参阅相应的文档：

   * **APNS**：[服务的质量](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW5) (Quality of Service)
   * **FCM**： [信息的生命周期](https://firebase.google.com/docs/cloud-messaging/concept-options#lifetime)

## 我的推送消息为何会被截断，或为何不能展开？

对于某些 Android 设备，您可能需要使用 `NotificationCompat.BigTextStyle` 来显示消息。