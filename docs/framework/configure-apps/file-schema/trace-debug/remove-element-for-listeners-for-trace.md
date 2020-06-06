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
# <a name="remove-element-for-listeners-for-trace"></a><span data-ttu-id="48455-102">\<remove>\<listeners>For 的元素\<trace></span><span class="sxs-lookup"><span data-stu-id="48455-102">\<remove> Element for \<listeners> for \<trace></span></span>
<span data-ttu-id="48455-103">從接聽**項集合中**移除接聽程式。</span><span class="sxs-lookup"><span data-stu-id="48455-103">Removes a listener from the **Listeners** collection.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**

## <a name="syntax"></a><span data-ttu-id="48455-104">語法</span><span class="sxs-lookup"><span data-stu-id="48455-104">Syntax</span></span>  
  
```xml  
<remove name="listener name" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="48455-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="48455-105">Attributes and Elements</span></span>  
 <span data-ttu-id="48455-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="48455-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="48455-107">屬性</span><span class="sxs-lookup"><span data-stu-id="48455-107">Attributes</span></span>  
  
|<span data-ttu-id="48455-108">屬性</span><span class="sxs-lookup"><span data-stu-id="48455-108">Attribute</span></span>|<span data-ttu-id="48455-109">描述</span><span class="sxs-lookup"><span data-stu-id="48455-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="48455-110">**name**</span><span class="sxs-lookup"><span data-stu-id="48455-110">**name**</span></span>|<span data-ttu-id="48455-111">必要屬性。</span><span class="sxs-lookup"><span data-stu-id="48455-111">Required attribute.</span></span><br /><br /> <span data-ttu-id="48455-112">要從接聽**項集合中**移除的接聽程式名稱。</span><span class="sxs-lookup"><span data-stu-id="48455-112">The name of the listener to remove from the **Listeners** collection.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="48455-113">子元素</span><span class="sxs-lookup"><span data-stu-id="48455-113">Child Elements</span></span>  
 <span data-ttu-id="48455-114">無。</span><span class="sxs-lookup"><span data-stu-id="48455-114">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="48455-115">父項目</span><span class="sxs-lookup"><span data-stu-id="48455-115">Parent Elements</span></span>  
  
|<span data-ttu-id="48455-116">元素</span><span class="sxs-lookup"><span data-stu-id="48455-116">Element</span></span>|<span data-ttu-id="48455-117">描述</span><span class="sxs-lookup"><span data-stu-id="48455-117">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="48455-118">通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。</span><span class="sxs-lookup"><span data-stu-id="48455-118">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`listeners`|<span data-ttu-id="48455-119">指定收集、儲存及路由傳送訊息的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="48455-119">Specifies a listener that collects, stores, and routes messages.</span></span> <span data-ttu-id="48455-120">接聽程式會將追蹤輸出導向至適當的目標。</span><span class="sxs-lookup"><span data-stu-id="48455-120">Listeners direct the tracing output to an appropriate target.</span></span>|  
|`system.diagnostics`|<span data-ttu-id="48455-121">指定用於收集、儲存及路由傳送訊息的追蹤接聽項，以及設定追蹤參數的層級。</span><span class="sxs-lookup"><span data-stu-id="48455-121">Specifies trace listeners that collect, store, and route messages and the level where a trace switch is set.</span></span>|  
|`trace`|<span data-ttu-id="48455-122">設定 ASP.NET 追蹤服務。</span><span class="sxs-lookup"><span data-stu-id="48455-122">Configures the ASP.NET trace service.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="48455-123">備註</span><span class="sxs-lookup"><span data-stu-id="48455-123">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="48455-124"><xref:System.Diagnostics.DefaultTraceListener>從集合中移除 `Listeners` ，會改變 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> 、 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> 、 <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> 和方法的行為 <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="48455-124">Removing the <xref:System.Diagnostics.DefaultTraceListener> from the `Listeners` collection alters the behavior of the <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType>, and <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> methods.</span></span> <span data-ttu-id="48455-125">呼叫 `Assert` 或 `Fail` 方法通常會導致訊息方塊顯示，但如果不 <xref:System.Diagnostics.DefaultTraceListener> 在集合中，則不會顯示訊息方塊 `Listeners` 。</span><span class="sxs-lookup"><span data-stu-id="48455-125">Calling an `Assert` or `Fail` method normally results in the display of a message box, however the message box is not displayed if the <xref:System.Diagnostics.DefaultTraceListener> is not in the `Listeners` collection.</span></span>  
  
## <a name="example"></a><span data-ttu-id="48455-126">範例</span><span class="sxs-lookup"><span data-stu-id="48455-126">Example</span></span>  
 <span data-ttu-id="48455-127">下列範例顯示如何從追蹤接聽項集合中移除預設**的追蹤接聽**程式。</span><span class="sxs-lookup"><span data-stu-id="48455-127">The following example shows how to remove the default trace listener from the trace **Listeners** collection.</span></span>  
  
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
  
## <a name="see-also"></a><span data-ttu-id="48455-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="48455-128">See also</span></span>

- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- [<span data-ttu-id="48455-129">追蹤和偵錯設定結構描述</span><span class="sxs-lookup"><span data-stu-id="48455-129">Trace and Debug Settings Schema</span></span>](index.md)
