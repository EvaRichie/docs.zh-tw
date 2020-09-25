---
title: <source> 項目
ms.date: 09/29/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source
- http://schemas.microsoft.com/.NetConfiguration/v2.0#source
helpviewer_keywords:
- <source> element
- source element
ms.openlocfilehash: e9c6a06ca9e481ecc2277e1d1ea76a0b99edb158
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173818"
---
# <a name="source-element"></a><span data-ttu-id="59c42-102">\<source> 項目</span><span class="sxs-lookup"><span data-stu-id="59c42-102">\<source> Element</span></span>

<span data-ttu-id="59c42-103">指定起始追蹤訊息的追蹤來源。</span><span class="sxs-lookup"><span data-stu-id="59c42-103">Specifies a trace source that initiates tracing messages.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<sources>**](sources-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<source>**

## <a name="syntax"></a><span data-ttu-id="59c42-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="59c42-104">Syntax</span></span>  
  
```xml  
<source>
  <listeners>...</listeners>  
</source>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="59c42-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="59c42-105">Attributes and Elements</span></span>  

 <span data-ttu-id="59c42-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="59c42-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="59c42-107">屬性</span><span class="sxs-lookup"><span data-stu-id="59c42-107">Attributes</span></span>  
  
|<span data-ttu-id="59c42-108">屬性</span><span class="sxs-lookup"><span data-stu-id="59c42-108">Attribute</span></span>|<span data-ttu-id="59c42-109">描述</span><span class="sxs-lookup"><span data-stu-id="59c42-109">Description</span></span>|  
|---------------|-----------------|  
|`name`|<span data-ttu-id="59c42-110">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="59c42-110">Optional attribute.</span></span><br /><br /> <span data-ttu-id="59c42-111">指定追蹤來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="59c42-111">Specifies the name of the trace source.</span></span>|  
|`switchName`|<span data-ttu-id="59c42-112">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="59c42-112">Optional attribute.</span></span><br /><br /> <span data-ttu-id="59c42-113">指定應用程式中追蹤參數實例的名稱。</span><span class="sxs-lookup"><span data-stu-id="59c42-113">Specifies the name of a trace switch instance in the application.</span></span> <span data-ttu-id="59c42-114">如果在專案中找不到參數 `<switches>` ，則值會指定參數的層級。</span><span class="sxs-lookup"><span data-stu-id="59c42-114">If the switch is not identified in a `<switches>` element, the value specifies the level for the switch.</span></span>|  
|`switchType`|<span data-ttu-id="59c42-115">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="59c42-115">Optional attribute.</span></span><br /><br /> <span data-ttu-id="59c42-116">指定追蹤參數的類型。</span><span class="sxs-lookup"><span data-stu-id="59c42-116">Specifies the type of the trace switch.</span></span> <span data-ttu-id="59c42-117">如果存在，類型必須是有效的類別名稱，而且不可以是空字串。</span><span class="sxs-lookup"><span data-stu-id="59c42-117">If present, the type must be a valid class name and cannot be an empty string.</span></span>|  
|`extraAttribute`|<span data-ttu-id="59c42-118">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="59c42-118">Optional attribute.</span></span><br /><br /> <span data-ttu-id="59c42-119">針對追蹤來源的方法所識別的追蹤來源特定屬性，指定其值 <xref:System.Diagnostics.TraceSource.GetSupportedAttributes%2A> 。</span><span class="sxs-lookup"><span data-stu-id="59c42-119">Specifies the value for a trace source-specific attribute identified by the <xref:System.Diagnostics.TraceSource.GetSupportedAttributes%2A> method for that trace source.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="59c42-120">子元素</span><span class="sxs-lookup"><span data-stu-id="59c42-120">Child Elements</span></span>  
  
|<span data-ttu-id="59c42-121">項目</span><span class="sxs-lookup"><span data-stu-id="59c42-121">Element</span></span>|<span data-ttu-id="59c42-122">描述</span><span class="sxs-lookup"><span data-stu-id="59c42-122">Description</span></span>|  
|-------------|-----------------|  
|[\<listeners>](listeners-element-for-source.md)|<span data-ttu-id="59c42-123">包含收集、儲存和路由傳送訊息的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="59c42-123">Contains listeners that collect, store, and route messages.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="59c42-124">父項目</span><span class="sxs-lookup"><span data-stu-id="59c42-124">Parent Elements</span></span>  
  
|<span data-ttu-id="59c42-125">項目</span><span class="sxs-lookup"><span data-stu-id="59c42-125">Element</span></span>|<span data-ttu-id="59c42-126">描述</span><span class="sxs-lookup"><span data-stu-id="59c42-126">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="59c42-127">通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。</span><span class="sxs-lookup"><span data-stu-id="59c42-127">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`system.diagnostics`|<span data-ttu-id="59c42-128">指定用於收集、儲存及路由傳送訊息的追蹤接聽項，以及設定追蹤參數的層級。</span><span class="sxs-lookup"><span data-stu-id="59c42-128">Specifies trace listeners that collect, store, and route messages and the level where a trace switch is set.</span></span>|  
|`sources`|<span data-ttu-id="59c42-129">包含起始追蹤訊息的追蹤來源。</span><span class="sxs-lookup"><span data-stu-id="59c42-129">Contains trace sources that initiate tracing messages.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="59c42-130">備註</span><span class="sxs-lookup"><span data-stu-id="59c42-130">Remarks</span></span>  

 <span data-ttu-id="59c42-131">此元素可用於電腦設定檔 ( # A0) 和應用程式佈建檔。</span><span class="sxs-lookup"><span data-stu-id="59c42-131">This element can be used in the machine configuration file (Machine.config) and the application configuration file.</span></span>  
  
## <a name="example"></a><span data-ttu-id="59c42-132">範例</span><span class="sxs-lookup"><span data-stu-id="59c42-132">Example</span></span>  

 <span data-ttu-id="59c42-133">下列範例示範如何使用專案 `<source>` 來加入追蹤來源 `mySource` ，以及設定名為之來源參數的層級 `sourceSwitch` 。</span><span class="sxs-lookup"><span data-stu-id="59c42-133">The following example shows how to use the `<source>` element to add the trace source `mySource` and to set the level for the source switch named `sourceSwitch`.</span></span> <span data-ttu-id="59c42-134">加入的主控台追蹤接聽程式會將追蹤資訊寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="59c42-134">A console trace listener is added that writes trace information to the console.</span></span>  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch" switchType="System.Diagnostics.SourceSwitch"  >  
        <listeners>  
          <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
            <filter type="System.Diagnostics.EventTypeFilter" initializeData="Error" />  
          </add>  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
        <switches>  
           <add name="sourceSwitch" value="Warning" />  
        </switches>
  </system.diagnostics>
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="59c42-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="59c42-135">See also</span></span>

- [<span data-ttu-id="59c42-136">追蹤和偵錯設定結構描述</span><span class="sxs-lookup"><span data-stu-id="59c42-136">Trace and Debug Settings Schema</span></span>](index.md)
- [<span data-ttu-id="59c42-137">追蹤參數</span><span class="sxs-lookup"><span data-stu-id="59c42-137">Trace Switches</span></span>](../../../debug-trace-profile/trace-switches.md)
