---
title: <system.web> 項目 (Web 設定)
ms.date: 03/30/2017
helpviewer_keywords:
- Web.config configuration file [ASP.NET]
- system.Web element
- <system.Web> element
- ASP.NET configuration system
- configuration files [ASP.NET]
ms.assetid: 24c4cf4f-ad32-42b2-b040-8e4549e2855e
ms.openlocfilehash: b37b05bdf90630251cbfcf86751243a3a8b77663
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152837"
---
# <a name="systemweb-element-web-settings"></a>\<system.web> 項目 (Web 設定)
包含 ASP.NET 裝載層如何管理整個進程行為的相關資訊。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;**\<system.web>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<system.web>  
</system.web>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  

無。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<applicationPool>](applicationpool-element-web-settings.md)|在 aspnet .config 檔案中指定 IIS 應用程式集區的配置設定。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<configuration>](../configuration-element.md)|指定通用語言執行時間和 .NET Framework 應用程式所使用之每個設定檔中的根項目。|  
  
## <a name="remarks"></a>備註  

`system.web`元素及其子專案 `applicationPool` 已加入至 .NET Framework，從 .NET FRAMEWORK 3.5 SP1。 當您在整合模式中執行 IIS 7.0 或更新版本時，此元素組合可讓您設定 ASP.NET 管理執行緒的方式，以及當 ASP.NET 裝載于 IIS 應用程式集區時，如何將要求排入佇列。 如果您以傳統或 ISAPI 模式執行 IIS 7.0 或更新版本，則會忽略這些設定。  
  
## <a name="example"></a>範例  

下列範例顯示當 ASP.NET 裝載于 IIS 應用程式集區時，如何在 aspnet .config 檔案中設定 ASP.NET 全進程行為。 此範例假設 IIS 是在整合模式中執行，且應用程式使用 .NET Framework 3.5 SP1 或更新版本。 這種行為不會發生在 .NET Framework 3.5 SP1 之前的 .NET Framework 版本中。 範例中的值為預設值。  
  
```xml  
<configuration>  
  <system.web>  
    <applicationPool
        maxConcurrentRequestsPerCPU="5000"
        maxConcurrentThreadsPerCPU="0"
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## <a name="element-information"></a>項目資訊  
  
|||  
|-|-|  
|命名空間||  
|結構描述名稱||  
|驗證檔||  
|可以是空的||  
  
## <a name="see-also"></a>另請參閱

- [\<applicationPool>元素（Web 設定）](applicationpool-element-web-settings.md)
