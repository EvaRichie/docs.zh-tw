---
title: <disableCachingBindingFailures> 項目
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures
helpviewer_keywords:
- assemblies [.NET Framework],caching binding failures
- caching assembly binding failures
- <disableCachingBindingFailures> element
- disableCachingBindingFailures element
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
ms.openlocfilehash: 23633cb282b8e59b4df4bcc2cd38717d805a207e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73117504"
---
# <a name="disablecachingbindingfailures-element"></a>\<disableCachingBindingFailures> 項目
指定是否要停用發生的系結失敗快取，因為探查找不到元件。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<disableCachingBindingFailures>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|已啟用|必要屬性。<br /><br /> 指定是否要停用發生的系結失敗快取，因為探查找不到元件。|  
  
## <a name="enabled-attribute"></a>啟用屬性  
  
|值|描述|  
|-----------|-----------------|  
|0|請勿停用發生的系結失敗快取，因為探查找不到元件。 從 .NET Framework 版本2.0 開始，這是預設的系結行為。|  
|1|停用發生的系結失敗快取，因為探查找不到元件。 此設定會還原為 .NET Framework 版本1.1 的系結行為。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`runtime`|包含有關組件繫結和記憶體回收的資訊。|  
  
## <a name="remarks"></a>備註  
 從 .NET Framework 版本2.0 開始，載入元件的預設行為是快取所有的系結和載入失敗。 也就是說，如果嘗試載入元件失敗，後續載入相同元件的要求會立即失敗，而不會嘗試找出元件。 這個元素會針對發生的系結失敗停用預設行為，因為在探查路徑中找不到該元件。 這些失敗會擲回 <xref:System.IO.FileNotFoundException> 。  
  
 某些系結和載入失敗不會受到此元素的影響，而且一律會進行快取。 因為找到元件，但無法載入，所以會發生這些失敗。 它們會擲回 <xref:System.BadImageFormatException> 或 <xref:System.IO.FileLoadException> 。 下列清單包含一些這類失敗的範例。  
  
- 如果您嘗試載入的檔案不是有效的元件，則後續載入元件的嘗試將會失敗，即使錯誤的檔案已被正確的元件取代也一樣。  
  
- 如果您嘗試載入由檔案系統鎖定的元件，則即使檔案系統釋放元件之後，載入元件的後續嘗試也會失敗。  
  
- 如果您嘗試載入的一個或多個元件版本是在探查路徑中，但您要求的特定版本不在其中，則後續嘗試載入該版本的動作將會失敗，即使將正確的版本移入探查路徑也一樣。  
  
## <a name="example"></a>範例  
 下列範例示範如何停用因為探查找不到元件而發生的元件系結失敗的快取。  
  
```xml  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [執行時間設定架構](index.md)
- [設定檔架構](../index.md)
- [執行階段如何找出組件](../../../deployment/how-the-runtime-locates-assemblies.md)
