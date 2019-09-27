---
description: 具有促销 eVar 和产品特定事件的产品变量示例。
seo-description: 具有促销 eVar 和产品特定事件的产品变量示例。
seo-title: 具有促销 eVar 和产品特定事件的产品变量
solution: Marketing Cloud,Analytics
title: 具有促销 eVar 和产品特定事件的产品变量
topic: 开发人员和实施
uuid: 94e882e4-b19d-4c48-9dfb-331465490347
translation-type: tm+mt
source-git-commit: b630c5cf09be7fbe31018cbf50564001eb6e2a5a

---


# Products variable with merchandising eVars and product-specific events{#products-variable-with-merchandising-evars-and-product-specific-events}

具有促销 eVar 和产品特定事件的产品变量示例。

```
//create a context data dictionary 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
  
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata["&&events"] = "event1 "; 
cdata["&&products"] = ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"; 
cdata["m.purchaseid"] = "1234567890"; 
cdata["m.purchase"] = "1"; 
  
var ADB = ADBMobile; 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
ADB.Analytics.trackAction("purchase", cdata); 
// trackState example: 
ADB.Analytics.trackState("Order Confirmation", cdata);
```

>[!TIP]
>
>If you trigger a product-specific event using the  variable, you must also set that event in the  variable, otherwise the event is filtered out during processing.*`&&products`**`&&events`*

