---
description: '在配置报表套件和收集Android应用程序数据之前，请完成以下先决条件 '
seo-description: '在配置报表套件和收集Android应用程序数据之前，请完成以下先决条件 '
seo-title: 开始之前
solution: Marketing Cloud，Analytics
title: 开始之前
topic: 开发人员和实施
uuid: 0ca9e937-8d40-4570-9dbf-9aece6eedf6
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Before you start {#before-you-start}

在配置报表包并收集 Android 应用程序数据之前，请完成以下先决任务：

## Role-specific tasks {#section_8B9EA1FA189F4C6DB7D829F0B5844FBC}

Analytics 管理员和应用程序开发人员必须完成以下任务：

### Analytics 管理员

要配置报表包并收集移动设备应用程序数据，请执行以下操作：

1. 完成[登录到 Adobe Mobile Services 用户界面](../getting-started/requirements.md#section_690A2EC4572E47869F183974E932A6A8)中的某一部分。
1. 为每个应用程序开发人员创建一个 Analytics 帐户。

此时应用程序开发人员便拥有查看您创建的报表包的权限。

>[!IMPORTANT]
>
>要创建新的报表包并下载SDK，您必须是Analytics管理员。

### 应用程序开发人员

1. 确保 Analytics 管理员已完成[特定于角色的任务](../getting-started/requirements.md#section_8B9EA1FA189F4C6DB7D829F0B5844FBC)中的“Analytics 管理员”**&#x200B;部分的步骤。

1. 确认 Analytics 管理员已完成[登录到 Adobe Mobile Services 用户界面](../getting-started/requirements.md#section_690A2EC4572E47869F183974E932A6A8)中的某一部分。
1. 配置报表包后，完成[下载 SDK](../getting-started/requirements.md#section_044C17DF82BC4FD8A3E409C456CE9A46) 中的步骤。

有关角色和权限的更多信息，请参阅[角色和权限](/help/using/gs/c-mob-roles-and-permissions.md)。

## 登录到 Adobe Mobile Services 用户界面 {#section_690A2EC4572E47869F183974E932A6A8}

Adobe Mobile Services 是用于移动设备应用程序分析和定位的主要报表界面。完成这些步骤后，您可以下载预先配置了数据收集服务器、报表包及许多其他设置的配置文件。

您可以使用以下方法之一登录到 Adobe Mobile Services 用户界面：

### Experience Cloud

使用您的 Adobe ID 登录到 [Experience Cloud](https://marketing.adobe.com)。此方法假定您的公司已在 Experience Cloud 中进行配置，并且您已经关联 Analytics 帐户。有关更多信息，请参阅 [管理Experience Cloud用户和产品](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/admin-getting-started.html)。

>[!TIP]
>
>如果您不确定您的公司是否已在Experience Cloud中供应，请使用您现有的Adobe Analytics帐户。

### Adobe Analytics

单击&#x200B;**[!UICONTROL 使用 Analytics 登录]**&#x200B;并输入您的 Analytics 公司名称、用户名和密码。

## 创建报表包 {#section_7BC602ED1ABA42C6AB722F506B5219F3}

要创建报表包以收集应用程序数据并定义应用程序，请执行以下操作：

1. Click **[!UICONTROL Create New App]**.

   If you do not see this button, click **[!UICONTROL Manage Apps]** &gt; **[!UICONTROL Add]**.

1. In the **[!UICONTROL Report Suite]** drop-down, select **[!UICONTROL New Report Suite]**.

1. 输入应用程序的名称并选择一种报表包类型。

   例如，报表包 ID 为 `mycomobileappdev`。由于您需要为开发版本和生产版本分别设置不同的报表包和应用程序，因此在准备好设置生产版本时，可以重复这些步骤。
1. In **[!UICONTROL Report Suite ID]**, verify that your report suite name is displayed.
1. 在&#x200B;**[!UICONTROL 从以下来源复制设置]**&#x200B;中，确认已选中&#x200B;**移动设备应用程序模板[!UICONTROL 。]**

   此模板将启用时间戳以收集离线数据，并激活移动设备解决方案变量以捕获生命周期量度。

1. Select your time zone, your currency, and click **[!UICONTROL Save]**.

## 下载 SDK {#section_044C17DF82BC4FD8A3E409C456CE9A46}

要下载 Mobile SDK，请执行以下操作：

1. 登录到 Mobile Services 用户界面，然后通过以下方式之一打开应用程序：

   * 在&#x200B;**[!UICONTROL 所有应用程序]下拉列表中，选择您的应用程序。**
   * 在右侧窗格中，找到您的应用程序并将其打开。

1. Click **[!UICONTROL Manage App Settings]**.
1. 滚动到&#x200B;**[!UICONTROL 应用程序 SDK 下载]部分。**
1. 下载适用于您的平台的 SDK 和示例应用程序。

>[!TIP]
>
>您的应用程序的配置文件自动包含在SDK下载中，因此您无需单独下载该文件。但是，如果您已经下载了 SDK，并且想要获取更新的设置，则需要再次下载配置文件。

如果您使用的是 Android Studio，则还可以将以下内容添加到应用程序的 `build.gradle` 文件中：

```java
compile 'com.adobe.mobile:adobeMobileLibrary:4.13.7'
```

请牢记以下信息：

* 将代码示例中的版本号替换为 Android SDK 的相应版本。
* 下载配置文件，并将其包含在您的项目中。