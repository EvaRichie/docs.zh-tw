---
title: <remove><listeners>For 的元素<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/remove
helpviewer_keywords:
- remove element
- <remove> element
ms.assetid: 9a5cd1b5-be1a-485f-8f0c-2890ad3ef3e0
ms.openlocfilehash: f06973ec30d5061e4a200d6bf7e68adcf6302018
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74088841"
---
# <a name="remove-element-for-listeners-for-trace"></a>\<remove>\<listeners>For 的元素\<trace>
從接聽**項集合中**移除接聽程式。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**

## <a name="syntax"></a>語法  
  
```xml  
<remove name="listener name" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|**name**|必要屬性。<br /><br /> 要從接聽**項集合中**移除的接聽程式名稱。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`listeners`|指定收集、儲存及路由傳送訊息的接聽程式。 接聽程式會將追蹤輸出導向至適當的目標。|  
|`system.diagnostics`|指定用於收集、儲存及路由傳送訊息的追蹤接聽項，以及設定追蹤參數的層級。|  
|`trace`|設定 ASP.NET 追蹤服務。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> <xref:System.Diagnostics.DefaultTraceListener>從集合中移除 `Listeners` ，會改變 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> 、 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> 、 <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> 和方法的行為 <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> 。 呼叫 `Assert` 或 `Fail` 方法通常會導致訊息方塊顯示，但如果不 <xref:System.Diagnostics.DefaultTraceListener> 在集合中，則不會顯示訊息方塊 `Listeners` 。  
  
## <a name="example"></a>範例  
 下列範例顯示如何從追蹤接聽項集合中移除預設**的追蹤接聽**程式。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <remove name="Default" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- [追蹤和偵錯設定結構描述](index.md)
