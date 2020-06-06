---
title: <ThrowUnobservedTaskExceptions> 項目
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ThrowUnobservedTaskExceptions element
- <ThrowUnobservedTaskExceptions> element
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
ms.openlocfilehash: de5a686bcbd88fc52173b488103f033575623d62
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153811"
---
# <a name="throwunobservedtaskexceptions-element"></a><span data-ttu-id="545a4-102">\<ThrowUnobservedTaskExceptions> 項目</span><span class="sxs-lookup"><span data-stu-id="545a4-102">\<ThrowUnobservedTaskExceptions> Element</span></span>
<span data-ttu-id="545a4-103">指定未處理的工作例外狀況是否應終止執行中的處理序。</span><span class="sxs-lookup"><span data-stu-id="545a4-103">Specifies whether unhandled task exceptions should terminate a running process.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<ThrowUnobservedTaskExceptions>**  
  
## <a name="syntax"></a><span data-ttu-id="545a4-104">語法</span><span class="sxs-lookup"><span data-stu-id="545a4-104">Syntax</span></span>  
  
```xml  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="545a4-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="545a4-105">Attributes and Elements</span></span>  
 <span data-ttu-id="545a4-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="545a4-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="545a4-107">屬性</span><span class="sxs-lookup"><span data-stu-id="545a4-107">Attributes</span></span>  
  
|<span data-ttu-id="545a4-108">屬性</span><span class="sxs-lookup"><span data-stu-id="545a4-108">Attribute</span></span>|<span data-ttu-id="545a4-109">描述</span><span class="sxs-lookup"><span data-stu-id="545a4-109">Description</span></span>|  
|---------------|-----------------|  
|`enabled`|<span data-ttu-id="545a4-110">必要屬性。</span><span class="sxs-lookup"><span data-stu-id="545a4-110">Required attribute.</span></span><br /><br /> <span data-ttu-id="545a4-111">指定未處理的工作例外狀況是否應終止正在執行的進程。</span><span class="sxs-lookup"><span data-stu-id="545a4-111">Specifies whether unhandled task exceptions should terminate the running process.</span></span>|  
  
## <a name="enabled-attribute"></a><span data-ttu-id="545a4-112">啟用屬性</span><span class="sxs-lookup"><span data-stu-id="545a4-112">enabled Attribute</span></span>  
  
|<span data-ttu-id="545a4-113">值</span><span class="sxs-lookup"><span data-stu-id="545a4-113">Value</span></span>|<span data-ttu-id="545a4-114">描述</span><span class="sxs-lookup"><span data-stu-id="545a4-114">Description</span></span>|  
|-----------|-----------------|  
|`false`|<span data-ttu-id="545a4-115">不會針對未處理的工作例外狀況終止正在執行的進程。</span><span class="sxs-lookup"><span data-stu-id="545a4-115">Does not terminate the running process for an unhandled task exception.</span></span> <span data-ttu-id="545a4-116">此為預設值。</span><span class="sxs-lookup"><span data-stu-id="545a4-116">This is the default.</span></span>|  
|`true`|<span data-ttu-id="545a4-117">針對未處理的工作例外狀況終止正在執行的進程。</span><span class="sxs-lookup"><span data-stu-id="545a4-117">Terminates the running process for an unhandled task exception.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="545a4-118">子元素</span><span class="sxs-lookup"><span data-stu-id="545a4-118">Child Elements</span></span>  
 <span data-ttu-id="545a4-119">無。</span><span class="sxs-lookup"><span data-stu-id="545a4-119">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="545a4-120">父項目</span><span class="sxs-lookup"><span data-stu-id="545a4-120">Parent Elements</span></span>  
  
|<span data-ttu-id="545a4-121">元素</span><span class="sxs-lookup"><span data-stu-id="545a4-121">Element</span></span>|<span data-ttu-id="545a4-122">描述</span><span class="sxs-lookup"><span data-stu-id="545a4-122">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="545a4-123">通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。</span><span class="sxs-lookup"><span data-stu-id="545a4-123">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`runtime`|<span data-ttu-id="545a4-124">包含有關執行階段初始化選項的資訊。</span><span class="sxs-lookup"><span data-stu-id="545a4-124">Contains information about runtime initialization options.</span></span>|  
|||  
  
## <a name="remarks"></a><span data-ttu-id="545a4-125">備註</span><span class="sxs-lookup"><span data-stu-id="545a4-125">Remarks</span></span>  
 <span data-ttu-id="545a4-126">如果未觀察到與相關聯的例外狀況 <xref:System.Threading.Tasks.Task> ，則不會有任何作業 <xref:System.Threading.Tasks.Task.Wait%2A> 、父代未附加，且屬性未被 <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> 讀取。工作例外狀況會被視為未觀察到。</span><span class="sxs-lookup"><span data-stu-id="545a4-126">If an exception that is associated with a <xref:System.Threading.Tasks.Task> has not been observed, there is no <xref:System.Threading.Tasks.Task.Wait%2A> operation, the parent is not attached, and the <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> property was not read the task exception is considered to be unobserved.</span></span>  
  
 <span data-ttu-id="545a4-127">在 .NET Framework 4 中，根據預設，如果已進行垃圾收集，則完成項會擲回 <xref:System.Threading.Tasks.Task> 例外狀況並終止進程。</span><span class="sxs-lookup"><span data-stu-id="545a4-127">In the .NET Framework 4, by default, if a <xref:System.Threading.Tasks.Task> that has an unobserved exception is garbage collected, the finalizer throws an exception and terminates the process.</span></span> <span data-ttu-id="545a4-128">進程的終止取決於垃圾收集和結束的時間。</span><span class="sxs-lookup"><span data-stu-id="545a4-128">The termination of the process is determined by the timing of garbage collection and finalization.</span></span>  
  
 <span data-ttu-id="545a4-129">為了讓開發人員更容易撰寫以工作為基礎的非同步程式碼，.NET Framework 4.5 會變更未觀察到例外狀況的這個預設行為。</span><span class="sxs-lookup"><span data-stu-id="545a4-129">To make it easier for developers to write asynchronous code based on tasks, the .NET Framework 4.5 changes this default behavior for unobserved exceptions.</span></span> <span data-ttu-id="545a4-130">未觀察到例外狀況仍然會 <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> 引發事件，但根據預設，進程不會終止。</span><span class="sxs-lookup"><span data-stu-id="545a4-130">Unobserved exceptions still cause the <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> event to be raised, but by default, the process does not terminate.</span></span> <span data-ttu-id="545a4-131">而是在引發事件之後忽略例外狀況，而不論事件處理常式是否觀察到例外狀況。</span><span class="sxs-lookup"><span data-stu-id="545a4-131">Instead, the exception is ignored after the event is raised, regardless of whether an event handler observes the exception.</span></span>  
  
 <span data-ttu-id="545a4-132">在 .NET Framework 4.5 中，您可以使用應用程式佈建檔中的[ \<ThrowUnobservedTaskExceptions> 元素](throwunobservedtaskexceptions-element.md)，以啟用擲回例外狀況的 .NET Framework 4 行為。</span><span class="sxs-lookup"><span data-stu-id="545a4-132">In the .NET Framework 4.5, you can use the [\<ThrowUnobservedTaskExceptions> element](throwunobservedtaskexceptions-element.md) in an application configuration file to enable the .NET Framework 4 behavior of throwing an exception.</span></span>  
  
 <span data-ttu-id="545a4-133">您也可以利用下列其中一種方式來指定例外狀況行為：</span><span class="sxs-lookup"><span data-stu-id="545a4-133">You can also specify the exception behavior in one of the following ways:</span></span>  
  
- <span data-ttu-id="545a4-134">藉由設定環境變數 `COMPlus_ThrowUnobservedTaskExceptions` （ `set COMPlus_ThrowUnobservedTaskExceptions=1` ）。</span><span class="sxs-lookup"><span data-stu-id="545a4-134">By setting the environment variable `COMPlus_ThrowUnobservedTaskExceptions` (`set COMPlus_ThrowUnobservedTaskExceptions=1`).</span></span>  
  
- <span data-ttu-id="545a4-135">藉由在 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft 中設定 registry DWORD 值 ThrowUnobservedTaskExceptions = 1 \\ 。.Netframework 鍵。</span><span class="sxs-lookup"><span data-stu-id="545a4-135">By setting the registry DWORD value ThrowUnobservedTaskExceptions = 1 in the HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework key.</span></span>  
  
## <a name="example"></a><span data-ttu-id="545a4-136">範例</span><span class="sxs-lookup"><span data-stu-id="545a4-136">Example</span></span>  
 <span data-ttu-id="545a4-137">下列範例顯示如何使用應用程式佈建檔來啟用工作中的例外狀況擲回。</span><span class="sxs-lookup"><span data-stu-id="545a4-137">The following example shows how to enable the throwing of exceptions in tasks by using an application configuration file.</span></span>  
  
```xml  
<configuration>
    <runtime>
        <ThrowUnobservedTaskExceptions enabled="true"/>
    </runtime>
</configuration>  
```  
  
## <a name="example"></a><span data-ttu-id="545a4-138">範例</span><span class="sxs-lookup"><span data-stu-id="545a4-138">Example</span></span>  
 <span data-ttu-id="545a4-139">下列範例示範如何從工作擲回未觀察到例外狀況。</span><span class="sxs-lookup"><span data-stu-id="545a4-139">The following example demonstrates how an unobserved exception is thrown from a task.</span></span> <span data-ttu-id="545a4-140">程式碼必須以發行的程式的形式執行，才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="545a4-140">The code must be run as a released program to work correctly.</span></span>  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="545a4-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="545a4-141">See also</span></span>

- [<span data-ttu-id="545a4-142">執行時間設定架構</span><span class="sxs-lookup"><span data-stu-id="545a4-142">Runtime Settings Schema</span></span>](index.md)
- [<span data-ttu-id="545a4-143">設定檔架構</span><span class="sxs-lookup"><span data-stu-id="545a4-143">Configuration File Schema</span></span>](../index.md)
