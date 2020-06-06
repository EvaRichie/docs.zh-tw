---
title: <appDomainManagerType> 項目
ms.date: 03/30/2017
helpviewer_keywords:
- appDomainManagerType element
- <appDomainManagerType> element
ms.assetid: ae8d5a7e-e7f7-47f7-98d9-455cc243a322
ms.openlocfilehash: 8eb6129b3fafaeb81a94d5a4078e41a16583a226
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154419"
---
# <a name="appdomainmanagertype-element"></a>\<appDomainManagerType> 項目
針對預設應用程式網域，指定做為應用程式網域管理員的類型。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<appDomainManagerType>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<appDomainManagerAssembly
   value="type name" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`value`|必要屬性。 指定類型的名稱，包括命名空間，做為進程中預設應用程式域的應用程式域管理員。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`runtime`|包含有關組件繫結和記憶體回收的資訊。|  
  
## <a name="remarks"></a>備註  
 若要指定應用程式域管理員的類型，您必須同時指定這個元素和專案 [\<appDomainManagerAssembly>](appdomainmanagerassembly-element.md) 。 如果未指定任何一個專案，則會忽略另一個元素。  
  
 載入預設應用程式域時， <xref:System.TypeLoadException> 如果指定的型別不存在於元素所指定的元件中，就會擲回， [\<appDomainManagerAssembly>](appdomainmanagerassembly-element.md) 而且進程無法啟動。  
  
 當您針對預設應用程式域指定應用程式域管理員類型時，從預設應用程式域建立的其他應用程式域會繼承應用程式域管理員類型。 使用 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType> 和 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType> 屬性，為新的應用程式域指定不同的應用程式域管理員類型。  
  
 指定應用程式域管理員類型時，應用程式必須具有完全信任。 （例如，在桌面上執行的應用程式會有完全信任）。如果應用程式沒有完全信任， <xref:System.TypeLoadException> 則會擲回。  
  
 類型和命名空間的格式與用於屬性的格式相同 <xref:System.Type.FullName%2A?displayProperty=nameWithType> 。  
  
 此 configuration 元素僅適用于 .NET Framework 4 和更新版本。  
  
## <a name="example"></a>範例  
 下列範例示範如何指定進程的預設應用程式域的應用程式域管理員是 `MyMgr` 元件中的類型 `AdMgrExample` 。  
  
```xml  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType>
- <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType>
- [\<appDomainManagerAssembly>元素](appdomainmanagerassembly-element.md)
- [執行時間設定架構](index.md)
- [設定檔架構](../index.md)
- [SetAppDomainManagerType 方法](../../../unmanaged-api/hosting/iclrcontrol-setappdomainmanagertype-method.md)
