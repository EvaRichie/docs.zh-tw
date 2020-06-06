---
title: <httpWebRequest> 項目 (網路設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: d33dadc14510feb00e05ca557b507b0cf8fa0dd0
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74087462"
---
# <a name="httpwebrequest-element-network-settings"></a>\<httpWebRequest> 項目 (網路設定)
自訂 Web 要求參數。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<httpWebRequest>**

## <a name="syntax"></a>語法  
  
```xml  
<httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|**屬性**|**說明**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|指定回應標頭的最大長度（以 kb 為單位）。 預設值為 64。 -1 值表示回應標頭上不會加諸大小限制。|  
|`maximumErrorResponseLength`|指定錯誤回應的最大長度（以 kb 為單位）。 預設值為 64。 值為-1 表示不會對錯誤回應施加任何大小限制。|  
|`maximumUnauthorizedUploadLength`|指定上傳以回應未授權錯誤碼的最大長度（以位元組為單位）。 預設值為 -1。 -1 的值表示不會對上載加諸任何大小限制。|  
|`useUnsafeHeaderParsing`|指定是否啟用不安全的標頭剖析。 預設值是 `false`。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|**元素**|**說明**|  
|-----------------|---------------------|  
|[設定](settings-element-network-settings.md)|為 <xref:System.Net> 命名空間設定基本的網路選項。|  
  
## <a name="remarks"></a>備註  
 根據預設，.NET Framework 會嚴格地強制執行 RFC 2616 以進行 URI 剖析。 某些伺服器回應可能會在禁止的欄位中包含控制字元，而這會導致 <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> 方法擲回 <xref:System.Net.WebException> 。 如果**useUnsafeHeaderParsing**設定為**true**， <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> 在此情況下將不會擲回; 不過，您的應用程式會很容易受到數種形式的 URI 剖析攻擊。 最佳的解決方法是變更伺服器，讓回應不包含控制字元。  
  
## <a name="configuration-files"></a>組態檔  
 此項目可以用於應用程式組態檔或電腦組態檔 (Machine.config)。  
  
## <a name="example"></a>範例  
 下列範例顯示如何指定大於一般的標頭長度上限。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>
- [網路設定結構描述](index.md)
