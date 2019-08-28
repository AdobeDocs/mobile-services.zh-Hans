---
description: 您可以在 Android 应用程序中提供目标内容。
keywords: android；库；移动；sdk
seo-description: 您可以在 Android 应用程序中提供目标内容。
seo-title: 目标配置
solution: Marketing Cloud，Analytics
title: 目标配置
topic: 开发人员和实施
uuid: 09fe2c9c-7b60-49c3-bb9 d-36a30 ce7 c350
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Target configuration {#target-configuration}

您可以在 Android 应用程序中提供目标内容。

## Set the application context {#section_37CAE496FF894FCA821F7760605574CA}

**(必需)** 必须 `setContext()` 在主活动的 `onCreate()` 方法中一次调用该方法。

例如：

```java
@Override 
public void onCreate(Bundle savedInstanceState) { 
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.main); 
  Config.setContext(this.getApplicationContext()); 
}
```

如果您在实施 Analytics 或受众管理时已经添加此方法调用，则无需再次添加。