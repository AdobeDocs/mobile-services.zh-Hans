---
description: 此信息可帮助您将 Windows 8.1 通用应用商店 SDK 与 Adobe Analytics 配合使用。
seo-description: 此信息可帮助您将 Windows 8.1 通用应用商店 SDK 与 Adobe Analytics 配合使用。
seo-title: 分析方法
solution: Marketing Cloud，Analytics
title: 分析方法
topic: 开发人员和实施
uuid: 79db105c-216c-4061-97f3-a55954995 e67
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Analytics methods {#analytics-methods}

此信息可帮助您将 Windows 8.1 通用应用商店 SDK 与 Adobe Analytics 配合使用。

SDK目前支持多个Adobe Experience Cloud解决方案]，包括Analytics]、Target]和Audience Manager]。方法将根据解决方案来添加前缀。Analytics 方法具有“Analytics”前缀。

下面每个方法均可用来将数据发送至 Adobe Analytics 报表包。

>[!TIP]
>
>When you consume `winmd` methods from winJS (JavaScript), all methods automatically have their first letter lowercased.

* **trackState(WinJS：trackState)**

   通过可选的上下文数据跟踪应用程序状态。状态是指您的应用程序中提供的各种视图，例如“主页功能板”、“应用程序设置”、“购物车”等。这些状态与网站中的页面类似，而且 `TrackState` 调用会使页面查看次数递增。如果 `state` 为空，它会在报表中显示为“应用程序名称 应用程序版本 (内部版本)”。如果您在报表中看到该值，请确保在每个 `state` 调用中设置 `TrackState`。

   >[!TIP]
   >
   >这是增加页面视图的唯一跟踪调用。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackState(Platform::String ^state, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> ^contextData); 
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile;
      ADB.Analytics.trackState("loginScreen", null);
      ```

* **TrackAction(WinJS：trackAction)**

   跟踪您的应用程序中的操作。操作是指您的应用程序中发生的要测量的事件，例如“登录”、“横幅点按”、“信息源订阅”及其他量度。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackAction(Platform::String ^action, Windows::Foundation::Collections::IMap <Platform::String^, Platform::Object> ^contextData);
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile; 
      ADB.Analytics.trackAction("Button Click", null); 
      ```

* **getTrackingIdentifierAsync(WinJS：getTrackingIdentifierAsync)**

   返回自动为 Analytics 生成的访客标识符。这是一个应用程序特定的唯一访客 ID，在初次启动时生成，随后进行存储并一直使用下去。此 ID 会在应用程序升级期间保留，并在应用程序卸载后删除。

   * 下面是这种方法对应的语法：

      ```csharp
      static Windows::Foundation::IAsyncOperation<Platform::String^> ^GetTrackingIdentifierAsync(); 
      ```

   * 以下是这种方法的代码示例：

      ```js
      var trackingIdentifier; 
      ADBMobile.Analytics.getTrackingIdentifierAsync().then(function (trackingid) { 
         trackingIdentifier = trackingid; 
      });
      ```

* **trackLocation(WinJS：trackLocation)**

   发送当前的 x y 坐标。此方法还使用 `ADBMobileConfig.json` 文件中定义的目标点来确定作为参数提供的位置是否位于您的任何 POI 内。如果当前坐标位于定义的 POI 内，则会填充上下文数据变量，并随 `trackLocation` 调用发送该变量。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackLocation(double lat, double lon, double accuracy, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^contextData);
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile; 
      ADB.Analytics.trackLocation(47.60621, -122.33207, null);
      ```

* **trackLifeTimeValueHend(WinJS：trackLifeTimeValueHend)**

   向用户的生命周期值中添加 `amount`。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackLifetimeValueIncrease(float amount, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^contextData); 
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile; 
      ADB.Analytics.trackLifetimeValueIncrease(10, null); 
      ```

* **tracktimeactionStart(WinJS：tracktimeActionStart)**

   启动名为 `action` 的定时操作。如果对已启动的操作调用此方法，则将覆盖上一个定时操作。

   >[!TIP]
   >
   >这个调用不发送点击。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackTimedActionStart(Platform::String ^action, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^contextData);
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile; 
      ADB.Analytics.trackTimedActionStart("cartToCheckout", null); 
      ```

* **tracktimeactionUpdate(WinJS：tracktimeactionUpdate)**

   传入 `contextData`，以更新与给定 `action` 关联的上下文数据。`data` 传递的内容会附加到给定操作的现有数据中，如果已经定义了相同的键，则会覆盖数据 `action`。

   >[!TIP]
   >
   >这个调用不发送点击。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackTimedActionUpdate(Platform::String ^action, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^contextData); 
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile; 
      var contextData = new Windows.Foundation.Collections.PropertySet(); 
      contextData["quantity"] = 3; 
      ADB.Analytics.trackTimedActionUpdate("cartToCheckout", contextData); 
      ```

* **tracktimeactionExistsAsync(WinJS：tracktimeactionExistsAsync)**

   如果存在给定的定时操作，则返回 true；如果不存在给定的定时操作，则返回 false。

   * 下面是这种方法对应的语法：

      ```csharp
      static Windows::Foundation::IAsyncOperation<bool> ^TrackTimedActionExistsAsync(Platform::String ^action); 
      ```

   * 以下是这种方法的代码示例：

      ```js
      ADBMobile.Analytics.trackTimedActionExistsAsync("signUp").then(function (exists) { 
          actionExists = exists; 
      });
      ```

* **tracktimeactionEnd(WinJS：tracktimeactionEnd)**

   结束定时操作。

   * 下面是这种方法对应的语法：

      ```csharp
      static void TrackTimedActionEnd(Platform::String ^action);
      ```

   * 以下是这种方法的代码示例：

      ```js
      var ADB = ADBMobile; 
      ADB.Analytics.trackTimedActionEnd("cartToCheckout"); 
      ```

* **clearTrackingQueue(WinJS：clearTrackingQueue)**

   清除 Analytics 跟踪队列中所有存储的点击。

   * 下面是此消息的语法：

      ```csharp
      static void ClearTrackingQueue();
      ```

   * 下面是代码示例：

      ```js
      ADBMobile.Analytics.clearTrackingQueue();
      ```

* **getQueedSizeSync(WinJS：getQueedSizeSync)**

   返回 Analytics 队列中当前存储的点击量。

   * 下面是这种方法对应的语法：

      ```csharp
      static Windows::Foundation::IAsyncOperation<int> ^GetQueueSizeAsync();
      ```

   * 以下是这种方法的代码示例：

      ```js
      var queueSize; 
      ADBMobile.Analytics.getQueueSizeAsync().then(function (size) { 
          queueSize = size; 
      });
      ```