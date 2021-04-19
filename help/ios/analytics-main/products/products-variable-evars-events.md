---
description: 以下是一个具有促销 eVar 和产品特定事件的产品变量示例。
seo-description: 以下是一个具有促销 eVar 和产品特定事件的产品变量示例。
seo-title: 具有促销 eVar 和产品特定事件的产品变量
solution: Experience Cloud,Analytics
title: 具有促销 eVar 和产品特定事件的产品变量
topic-fix: Developer and implementation
uuid: f913211e-97ad-4237-bfe4-7ded01295caf
exl-id: f438190d-0d2d-4bcd-a1c7-156e46e61162
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 100%

---

# 具有促销 eVar 和产品特定事件的产品变量 {#products-variable-with-merchandising-evars-and-product-specific-events}

以下是一个具有促销 eVar 和产品特定事件的产品变量示例。

```
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
  
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
[contextData setObject:@"event1" forKey:@"&&events"]; 
[contextData setObject:@";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99" forKey:@"&&products"]; 
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"]; 
[contextData setObject:@"1" forKey:@"m.purchase"]; 
  
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
[ADBMobile trackAction:@"purchase" data:contextData]; 
// trackState example: 
[ADBMobile trackState:@"Order Confirmation" data:contextData];
```

>[!TIP]
>
>如果通过使用 *`&&products`* 变量触发产品特定事件，则还必须在 *`&&events`* 变量中设置该事件。如果未设置该事件，则会在处理期间将其过滤掉。
