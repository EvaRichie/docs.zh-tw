---
title: <extensions> 區段
ms.date: 03/30/2017
ms.assetid: 53a59fb6-dede-47ec-9384-b3c2e8f0c1fa
ms.openlocfilehash: f3eb5d446291dfa6b7c8e0f1ee2b6a5cf53c2162
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185778"
---
# <a name="extensions-section"></a>\<extensions> 區段

這個組態區段包含延伸的集合，可讓使用者建立使用者定義的繫結、行為和其他方面的延伸。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<extensions>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingExtensions>
    </bindingExtensions>
    <behaviorExtensions>
    </behaviorExtensions>
    <bindingElementExtensions>
    </bindingElementExtensions>
    <endpointExtensions>
    </endpointExtensions>
  </extensions>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  

 無。  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<behaviorExtensions>](behaviorextensions.md)|這個區段包含指定行為延伸的子項目，可讓使用者自訂服務或端點行為。|  
|[\<bindingElementExtensions>](bindingelementextensions.md)|這個區段會啟用電腦或應用程式組態檔中自訂繫結項目的使用。|  
|[\<bindingExtensions>](bindingextensions.md)|這個區段包含指定繫結延伸的子項目，可讓使用者自訂繫結。|  
|[\<endpointExtensions>](endpointextensions.md)|這個區段包含會註冊標準端點的子項目。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|system.ServiceModel|所有 WCF 組態項目的根項目。|
