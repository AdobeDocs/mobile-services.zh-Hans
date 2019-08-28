---
description: 以下是 Android 库提供的 Adobe Target 方法列表。
keywords: android；库；移动；sdk
seo-description: 以下是 Android 库提供的 Adobe Target 方法列表。
seo-title: 针对Android的Target方法
solution: Marketing Cloud，Analytics
title: 针对Android的Target方法
topic: 开发人员和实施
uuid: 8e9808b2-ba80-4646-ba05-8e62 d4 fde065
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# 针对Android的Target方法{#target-methods}

以下是 Android 库提供的 Adobe Target 方法列表。

SDK目前支持多个Adobe Experience Cloud解决方案，包括Analytics、Target、Audience Manager和Adobe Experience Platform Identity Service]。Methods are prefixed according to the solution. For example, Experience Cloud ID methods are prefixed with `target`.

>[!TIP]
>
>[生命周期量度](/help/android/metrics.md)将作为参数发送至每个 mbox 负载。

## Class reference : TargetLocationRequest {#section_A8CC898922164E819EC730DC92A6742B}

**属性：**

```java
public String name; 
public String defaultContent; 
public HashMap<String, Object> parameters;
```

**String常量**

>[!TIP]
>
>在为自定义参数设置键时，以下常量便于使用。

```java
public static final String TARGET_PARAMETER_ORDER_ID   = "orderId"; 
public static final String TARGET_PARAMETER_ORDER_TOTAL         = "orderTotal"; 
public static final String TARGET_PARAMETER_PRODUCT_PURCHASE_ID = "productPurchasedId"; 
public static final String TARGET_PARAMETER_CATEGORY_ID         = "categoryId"; 
public static final String TARGET_PARAMETER_MBOX_3RDPARTY_ID    = "mbox3rdPartyId"; 
public static final String TARGET_PARAMETER_MBOX_PAGE_VALUE     = "mboxPageValue"; 
public static final String TARGET_PARAMETER_MBOX_PC             = "mboxPC"; // pcId in cookie 
public static final String TARGET_PARAMETER_MBOX_SESSION_ID     = "mboxSession"; // sessionId in cookie 
public static final String TARGET_PARAMETER_MBOX_HOST           = "mboxHost";
```

>[!IMPORTANT]
>
>* If you are using SDKs **before** version 4.14.0, see [https://developers.adobetarget.com/api/#input-parameters](https://developers.adobetarget.com/api/#input-parameters) for parameters limitations.
   >
   >
* If you are using SDKs version 4.14.0 **or later**, see [https://developers.adobetarget.com/api/#batch-input-parameters](https://developers.adobetarget.com/api/#batch-input-parameters) for parameters limitations.


* **loadRequest**

   向您配置的 Target 服务器发送 request，并返回在块 callback 中生成的选件的字符串值。

   * 下面是这种方法对应的语法：

      ```java
      public static void loadRequest(TargetLocationRequest request, TargetCallback<String> callback);
      ```

   * 以下是这种方法的代码示例：

      ```java
      Target.loadRequest(heroBannerRequest, new Target.TargetCallback<String>() {  @Override  public void call(String item) {   // do something with item  } });
      ```

* **loadRequest**

   向您配置的 Target 服务器发送 request，并返回在块 callback 中生成的选件的字符串值。

   * 下面是这种方法对应的语法：

      ```java
      public static void loadRequest(final String name final String defaultContent, final Map `<String, Object>` profileParameters, 
                                     final Map `<String, Object>` orderParameters,final Map `<String Object>` mboxParameters, final TargetCallback<String> callback)
      ```

   * 以下是这种方法的代码示例：

      ```java
      Map `<String, Object>` profileParameters = new HashMap `<String, Object>`(); profileParameters.put(“profile-parameter-key”, “profile-parameter-value”); 
      Map `<String, Object>` orderParameters = new HashMap `<String, Object>`(); orderParameters.put(“order-parameter-key”, “order-parameter-value”);
      Map `<String, Object>` mboxParameters = new HashMap `<String, Object>`(); 
      mboxParameters.put(“mbox-parameter-key”, “mbox-parameter-value”); 
      Target.loadRequest(“mboxName”, “defaultContent”, profileParameters, orderParameters, mboxParameters
      new TargetCallback<String>() {
          @Override
          public void call (String item) {
             Log.d(“Target Content”, item); 
          }
      });
      ```

* **loadRequest**

   向您配置的 Target 服务器发送请求，并返回在 TargetCallback 中生成的选件的字符串值。

   * 下面是这种方法对应的语法：

      ```java
      public static void loadRequest(final String name, final String defaultContent, final Map<String, Object> profileParameters, final Map<String, Object> orderParameters, final Map<String, Object> mboxParameters, final Map<String, Object> requestLocationParameters, final TargetCallback<String> callback);
      ```

   * **返回：** N/A

   * **参数：**

      以下是此方法的参数：

      * **name**

         要检索的 Target mbox/位置的名称。

         * **类型：** 字符串
      * **defaultContent**

         Target 服务器不可访问或用户不符合促销活动资格时，在回调中返回的值。

         * **类型：** 字符串
      * **profileParameters**

         该词典中的值将在对 Target 的请求中用于“profileParameters”对象。

         * **类型：** 地图 `<String, Object>`
      * **orderParameters**

         该词典中的值将在对 Target 的请求中用于“order”对象。

         * **类型：** 地图 `<String, Object>`
      * **mboxParameters**

         此词典中的值将进入Target请求。

         * **类型：** 地图 `<String, Object>`
      * **requestLocationParameters**

         该词典中的值将在对 Target 的请求中用于“requestLocation”对象。

         * **类型：** 地图 `<String, Object>`
      * **callback**

         此方法将通过来自 Target 服务器的选件内容进行调用。如果 Target 服务器不可访问，或者用户不符合促销活动资格，则将返回 defaultContent。

         * **类型：** targetCallback `<String>`
   * 下面是此方法的示例代码：

      ```java
      Map `<String, Object>` profileParameters = new HashMap `<String, Object>`(); profileParameters.put(“profile-parameter-key”, “profile-parameter-value”); 
      Map `<String, Object>` orderParameters = new HashMap `<String, Object>`(); orderParameters.put(“order-parameter-key”, “order-parameter-value”); 
      Map `<String, Object>` mboxParameters = new HashMap `<String, Object>`(); mboxParameters.put(“mbox-parameter-key”, “mbox-parameter-value”); 
      Map `<String, Object>` requestLocationParameters = new HashMap `<String, Object>`(); requestLocationParameters.put(“request-location-parameter-key”, “request-location-parameter-value”); 
      
      Target.loadRequest(“mboxName”, “defaultContent”, profileParameters, orderParameters, mboxParameters, requestLocationParameters,new TargetCallback<String>() {
         @Override
         public void call (String item) { 
            Log.d(“Target Content”, item);
         } 
      });
      ```

      有关基本 Target API 的更多信息，请参阅 Target 开发人员帮助中的 [Delivery](https://docs.adobe.com/dev/products/target/reference/delivery.html)（交付）。








* **createOrder&#x200B;ConfirmRequest**

   通过给定参数创建 TargetLocationRequest 对象。

   * 下面是这种方法对应的语法：

      ```java
      public static TargetLocationRequest createOrderConfirmRequest(String name, String orderId, String orderTotal, String productPurchasedId, Map<String, Object> parameters);
      ```

   * 以下是这种方法的代码示例：

      ```java
      TargetLocationRequest orderConfirm = Target.createOrderConfirmRequest("orderConfirm", "order", "47.88", "3722", null);
      ```

* **createRequest**

   通过给定参数创建 TargetLocationRequest 对象。

   * 下面是这种方法对应的语法：

      ```java
      public static TargetLocationRequest createRequest(String name, String defaultContent, Map<String, Object> parameters);
      ```

   * 以下是这种方法的代码示例：

      ```java
      TargetLocationRequest heroBannerRequest = Target.createRequest("heroBanner", "default.png", null);
      ```

* **clearCookies**

   清除应用程序中的任何目标 Cookie。

   * 下面是这种方法对应的语法：

      ```java
      public static void clearCookies();
      ```

   * 以下是这种方法的代码示例：

      ```java
      Target.clearCookies();
      ```

* **getPcID**

   返回 pcID。

   * 下面是这种方法对应的语法：

      ```java
      public static String getPcID();
      ```

   * 以下是这种方法的代码示例：

      ```java
      Target.getPcID();
      ```

* **getSessionID**

   返回会话 ID。

   * 下面是这种方法对应的语法：

      ```java
      public static String getSessionID();
      ```

   * 以下是这种方法的代码示例：

      ```java
      Target.getSessionID();
      ```

* **setThirdPartyID**

   设置第三方 ID。

   * 下面是这种方法对应的语法：

      ```java
      public static String setThirdPartyID(final String thirdPartyId);
      ```

   * 以下是这种方法的代码示例：

      ```java
      Target.setThirdPartyID(“third-party-id”);
      ```

* **getThirdPartyID**

   返回第三方 ID。

   * 下面是这种方法对应的语法：

      ```java
      public static String getThirdPartyID();
      ```

   * 以下是这种方法的代码示例：

      ```java
      String thirdPartyId = Target.getThirdPartyID();
      ```