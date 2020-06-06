---
title: <system.runtime.caching> 項目 (快取設定)
ms.date: 03/30/2017
helpviewer_keywords:
- <system.runtime.caching> element
- caching [.NET Framework], configuration
- system.runtime.caching element
ms.assetid: 9b44daee-874a-4bd1-954e-83bf53565590
ms.openlocfilehash: df4887c8801dcf8af06b3826673a03cbc7dbc9b5
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153850"
---
# <a name="systemruntimecaching-element-cache-settings"></a><span data-ttu-id="181a6-102">\<system.runtime.caching> 項目 (快取設定)</span><span class="sxs-lookup"><span data-stu-id="181a6-102">\<system.runtime.caching> Element (Cache Settings)</span></span>

<span data-ttu-id="181a6-103">透過組態檔中的 <xref:System.Runtime.Caching.ObjectCache> 項目，提供預設記憶體內 `memoryCache` 實作的組態。</span><span class="sxs-lookup"><span data-stu-id="181a6-103">Provides configuration for the default in-memory <xref:System.Runtime.Caching.ObjectCache> implementation through the `memoryCache` entry in the configuration file.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;**\<system.runtime.caching>**  
  
## <a name="syntax"></a><span data-ttu-id="181a6-104">語法</span><span class="sxs-lookup"><span data-stu-id="181a6-104">Syntax</span></span>  
  
```xml  
<system.runtime.caching >  
   <!-- child elements -->  
</system.runtime.caching >  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="181a6-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="181a6-105">Attributes and Elements</span></span>

<span data-ttu-id="181a6-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="181a6-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="181a6-107">屬性</span><span class="sxs-lookup"><span data-stu-id="181a6-107">Attributes</span></span>

`None`  

### <a name="child-elements"></a><span data-ttu-id="181a6-108">子元素</span><span class="sxs-lookup"><span data-stu-id="181a6-108">Child Elements</span></span>

|<span data-ttu-id="181a6-109">元素</span><span class="sxs-lookup"><span data-stu-id="181a6-109">Element</span></span>|<span data-ttu-id="181a6-110">描述</span><span class="sxs-lookup"><span data-stu-id="181a6-110">Description</span></span>|  
|-------------|-----------------|  
|[\<memoryCache>](memorycache-element-cache-settings.md)|<span data-ttu-id="181a6-111">定義項目，這個項目會用來設定以 <xref:System.Runtime.Caching.MemoryCache> 類別為基礎的快取。</span><span class="sxs-lookup"><span data-stu-id="181a6-111">Defines an element that is used to configure a cache that is based on the <xref:System.Runtime.Caching.MemoryCache> class.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="181a6-112">父項目</span><span class="sxs-lookup"><span data-stu-id="181a6-112">Parent Elements</span></span>  
  
|<span data-ttu-id="181a6-113">元素</span><span class="sxs-lookup"><span data-stu-id="181a6-113">Element</span></span>|<span data-ttu-id="181a6-114">描述</span><span class="sxs-lookup"><span data-stu-id="181a6-114">Description</span></span>|  
|-------------|-----------------|  
|[\<configuration>](../configuration-element.md)|<span data-ttu-id="181a6-115">指定通用語言執行時間和 .NET Framework 應用程式所使用之每個設定檔中的根項目。</span><span class="sxs-lookup"><span data-stu-id="181a6-115">Specifies the root element in every configuration file that is used by the common language runtime and .NET Framework applications.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="181a6-116">備註</span><span class="sxs-lookup"><span data-stu-id="181a6-116">Remarks</span></span>

<span data-ttu-id="181a6-117">這個命名空間中的類別提供如同在 ASP.NET 中使用快取設備的方式，但是不需要在 `System.Web` 組件上的相依性。</span><span class="sxs-lookup"><span data-stu-id="181a6-117">The classes in this namespace provide a way to use caching facilities like those in ASP.NET, but without a dependency on the `System.Web` assembly.</span></span> <span data-ttu-id="181a6-118">如需詳細資訊，請參閱 [Caching in .NET Framework Applications](../../../performance/caching-in-net-framework-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="181a6-118">For more information, see [Caching in .NET Framework Applications](../../../performance/caching-in-net-framework-applications.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="181a6-119">命名空間中的輸出快取功能和類型在 <xref:System.Runtime.Caching> .NET Framework 4 中是新的。</span><span class="sxs-lookup"><span data-stu-id="181a6-119">The output caching functionality and types in the <xref:System.Runtime.Caching> namespace are new in .NET Framework 4.</span></span>  
  
## <a name="example"></a><span data-ttu-id="181a6-120">範例</span><span class="sxs-lookup"><span data-stu-id="181a6-120">Example</span></span>

<span data-ttu-id="181a6-121">下列範例示範如何設定以 <xref:System.Runtime.Caching.MemoryCache> 類別為基礎的快取，</span><span class="sxs-lookup"><span data-stu-id="181a6-121">The following example shows how to configure a cache that is based on the <xref:System.Runtime.Caching.MemoryCache> class.</span></span> <span data-ttu-id="181a6-122">並示範如何設定記憶體快取之 `namedCaches` 項目的執行個體。</span><span class="sxs-lookup"><span data-stu-id="181a6-122">The example shows how to configure an instance of the `namedCaches` entry for memory cache.</span></span> <span data-ttu-id="181a6-123">快取的名稱會設定為預設快取專案名稱，方法是將 `name` 屬性設定為 "default"。</span><span class="sxs-lookup"><span data-stu-id="181a6-123">The name of the cache is set to the default cache entry name by setting the `name` attribute to "Default".</span></span>  
  
<span data-ttu-id="181a6-124">`cacheMemoryLimitMegabytes` 屬性和 `physicalMemoryPercentage` 屬性都設定為零。</span><span class="sxs-lookup"><span data-stu-id="181a6-124">The `cacheMemoryLimitMegabytes` attribute and the `physicalMemoryPercentage` attribute are set to zero.</span></span> <span data-ttu-id="181a6-125">將這些屬性設定為零表示預設會使用 <xref:System.Runtime.Caching.MemoryCache> 自動調整啟發學習法。</span><span class="sxs-lookup"><span data-stu-id="181a6-125">Setting these attributes to zero means that the <xref:System.Runtime.Caching.MemoryCache> autosizing heuristics are used by default.</span></span> <span data-ttu-id="181a6-126">快取實作應該會每隔兩分鐘即比較目前的記憶體負載與絕對和百分比型記憶體限制。</span><span class="sxs-lookup"><span data-stu-id="181a6-126">The cache implementation should compare the current memory load against the absolute and percentage-based memory limits every two minutes.</span></span>  
  
```xml  
<configuration>  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="Default"
               cacheMemoryLimitMegabytes="0"
               physicalMemoryLimitPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="181a6-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="181a6-127">See also</span></span>

- [<span data-ttu-id="181a6-128">\<memoryCache>元素（快取設定）</span><span class="sxs-lookup"><span data-stu-id="181a6-128">\<memoryCache> Element (Cache Settings)</span></span>](memorycache-element-cache-settings.md)
