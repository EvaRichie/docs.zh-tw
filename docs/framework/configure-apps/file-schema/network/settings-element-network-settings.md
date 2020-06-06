---
title: <settings> 項目 (網路設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#settings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings
helpviewer_keywords:
- settings element
- <settings> element
ms.assetid: 189ce989-c39b-427d-b004-6b82a668b931
ms.openlocfilehash: d510c445c585a36005ed415b14188efc4be03984
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74089111"
---
# <a name="settings-element-network-settings"></a>\<settings> 項目 (網路設定)
為 <xref:System.Net?displayProperty=nameWithType> 命名空間設定基本的網路選項。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<settings>**

## <a name="syntax"></a>語法  
  
```xml  
<settings>  
  <httpListener>...</httpListener>  
  <httpWebRequest>...</httpWebRequest>  
  <ipv6>...</ipv6>  
  <performanceCounters>...</performanceCounters>  
  <servicePointManager>...</servicePointManager>  
  <socket>...</socket>  
  <webProxyScript>...</webProxyScript>  
</settings>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
 無。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[HTTPListener](httplistener-element-network-settings.md)|自訂類別所使用的參數 <xref:System.Net.HttpListener> 。|  
|[HTTPWebRequest](httpwebrequest-element-network-settings.md)|自訂 Web 要求參數。|  
|[ipv4](ipv6-element-network-settings.md)|啟用網際網路通訊協定第6版（IPv6）支援。|  
|[\<performanceCounter>元素（網路設定）](performancecounter-element-network-settings.md)|啟用網路效能計數器。|  
|[servicePointManager](servicepointmanager-element-network-settings.md)|設定網路資源的連接。|  
|[插槽](socket-element-network-settings.md)|指定通訊端作業是否使用完成埠。|  
|[\<webProxyScript>元素（網路設定）](webproxyscript-element-network-settings.md)|設定用來探索 Web proxy 之腳本的特性。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[system.net](system-net-element-network-settings.md)|包含會指定 .NET Framework 如何連接至網路的設定。|  
  
## <a name="remarks"></a>備註  
  
## <a name="configuration-files"></a>組態檔  
 此項目可以用於應用程式組態檔或電腦組態檔 (Machine.config)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Net?displayProperty=nameWithType>
- [網路設定結構描述](index.md)
