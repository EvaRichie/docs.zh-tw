---
title: WCF 效能計數器
ms.date: 03/30/2017
helpviewer_keywords:
- performance counters [WCF]
ms.assetid: f559b2bd-ed83-4988-97a1-e88f06646609
ms.openlocfilehash: 7c8a134039526abf046136ac383fbaff3a5abbfe
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90541209"
---
# <a name="wcf-performance-counters"></a><span data-ttu-id="e573b-102">WCF 效能計數器</span><span class="sxs-lookup"><span data-stu-id="e573b-102">WCF Performance Counters</span></span>
<span data-ttu-id="e573b-103">Windows Communication Foundation (WCF) 包含一組大量的效能計數器，可協助您測量應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="e573b-103">Windows Communication Foundation (WCF) includes a large set of performance counters to help you gauge your application's performance.</span></span>  
  
## <a name="enabling-performance-counters"></a><span data-ttu-id="e573b-104">啟用效能計數器</span><span class="sxs-lookup"><span data-stu-id="e573b-104">Enabling Performance Counters</span></span>  
 <span data-ttu-id="e573b-105">您可以透過 WCF 服務的 app.config 設定檔啟用 WCF 服務的效能計數器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e573b-105">You can enable performance counters for a WCF service through the app.config configuration file of the WCF service as follows:</span></span>  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <diagnostics performanceCounters="All" />  
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="e573b-106">`performanceCounters` 屬性可設為啟用特定類型的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-106">The `performanceCounters` attribute can be set to enable a specific type of performance counters.</span></span> <span data-ttu-id="e573b-107">有效值為</span><span class="sxs-lookup"><span data-stu-id="e573b-107">Valid values are</span></span>  
  
- <span data-ttu-id="e573b-108">All：所有類別的計數器 (ServiceModelService、ServiceModelEndpoint 和 ServiceModelOperation) 都會啟用。</span><span class="sxs-lookup"><span data-stu-id="e573b-108">All: All category counters (ServiceModelService, ServiceModelEndpoint and ServiceModelOperation) are enabled.</span></span>  
  
- <span data-ttu-id="e573b-109">ServiceOnly：只啟用 ServiceModelService 類別的計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-109">ServiceOnly: Only ServiceModelService category counters are enabled.</span></span> <span data-ttu-id="e573b-110">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="e573b-110">This is the default value.</span></span>  
  
- <span data-ttu-id="e573b-111">Off：ServiceModel\* 效能計數器會停用。</span><span class="sxs-lookup"><span data-stu-id="e573b-111">Off: ServiceModel\* performance counters are disabled.</span></span>  
  
 <span data-ttu-id="e573b-112">如果您想要啟用所有 WCF 應用程式的效能計數器，您可以將設定設定放在 Machine.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="e573b-112">If you want to enable performance counters for all WCF applications, you can place the configuration settings in the Machine.config file.</span></span>  <span data-ttu-id="e573b-113">如需有關為電腦上的效能計數器設定足夠記憶體的詳細資訊，請參閱下面的 **效能計數器的增加記憶體大小** 一節。</span><span class="sxs-lookup"><span data-stu-id="e573b-113">Please see the **Increasing Memory Size for Performance Counters** section below for more information on configuring sufficient memory for performance counters on your machine.</span></span>  
  
 <span data-ttu-id="e573b-114">如果您使用 WCF 擴充性點，例如自訂作業啟動程式，您也應該發出自己的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-114">If you use WCF extensibility points such as custom operation invokers, you should also emit your own performance counters.</span></span> <span data-ttu-id="e573b-115">這是因為如果您執行了擴充點，WCF 可能不會再于預設路徑中發出標準效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="e573b-115">This is because if you implement an extensibility point, WCF may no longer emit the standard performance counter data in the default path.</span></span> <span data-ttu-id="e573b-116">如果您沒有實作手動效能計數器支援，可能無法看見預期的效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="e573b-116">If you do not implement manual performance counter support, you may not see the performance counter data you expect.</span></span>  
  
 <span data-ttu-id="e573b-117">您也可以在程式碼中啟用效能計數器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e573b-117">You can also enable performance counters in your code as follows,</span></span>  
  
```csharp
using System.Configuration;  
using System.ServiceModel.Configuration;  
using System.ServiceModel.Diagnostics;  
Configuration config = ConfigurationManager.OpenExeConfiguration(  
    ConfigurationUserLevel.None);  
ServiceModelSectionGroup sg = ServiceModelSectionGroup.GetSectionGroup(config);  
sg.Diagnostic.PerformanceCounters = PerformanceCounterScope.All;  
config.Save();  
```  
  
## <a name="viewing-performance-data"></a><span data-ttu-id="e573b-118">檢視效能資料</span><span class="sxs-lookup"><span data-stu-id="e573b-118">Viewing Performance Data</span></span>  
 <span data-ttu-id="e573b-119">若要檢視效能計數器所擷取的資料，您可以使用隨附於 Windows 的效能監視器 (Perfmon.exe)。</span><span class="sxs-lookup"><span data-stu-id="e573b-119">To view data captured by the performance counters, you can use the Performance Monitor (Perfmon.exe) that comes with Windows.</span></span> <span data-ttu-id="e573b-120">您可以藉由前往 [ **開始**]，然後按一下 [ **執行** ]，然後在對話方塊中輸入，來啟動這 `perfmon.exe` 項工具。</span><span class="sxs-lookup"><span data-stu-id="e573b-120">You can launch this tool by going to **Start**, and click **Run** and type `perfmon.exe` in the dialog box.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e573b-121">效能計數器執行個體可能會在端點發送器處理完成最後一個訊息之前釋出。</span><span class="sxs-lookup"><span data-stu-id="e573b-121">Performance counter instances may be released before the last messages have been processed by the endpoint dispatcher.</span></span> <span data-ttu-id="e573b-122">如此可能導致少數訊息的效能資料未能予以擷取</span><span class="sxs-lookup"><span data-stu-id="e573b-122">This can result in performance data not being captured for a few messages.</span></span>  
  
## <a name="increasing-memory-size-for-performance-counters"></a><span data-ttu-id="e573b-123">為效能計數器增加記憶體大小</span><span class="sxs-lookup"><span data-stu-id="e573b-123">Increasing Memory Size for Performance Counters</span></span>  
 <span data-ttu-id="e573b-124">WCF 針對其效能計數器類別使用不同的共用記憶體。</span><span class="sxs-lookup"><span data-stu-id="e573b-124">WCF uses separate shared memory for its performance counter categories.</span></span>  
  
 <span data-ttu-id="e573b-125">根據預設，不同的共用記憶體會設為全域效能計數器記憶體的四分之一。</span><span class="sxs-lookup"><span data-stu-id="e573b-125">By default, separate shared memory is set to a quarter the size of global performance counter memory.</span></span> <span data-ttu-id="e573b-126">預設的全域效能計數器記憶體為 524,288 個位元組。</span><span class="sxs-lookup"><span data-stu-id="e573b-126">The default global performance counter memory is 524,288 bytes.</span></span> <span data-ttu-id="e573b-127">因此，三個 WCF 效能計數器類別的預設大小為大約128KB。</span><span class="sxs-lookup"><span data-stu-id="e573b-127">Therefore, the three WCF performance counter categories have a default size of approximately 128KB each.</span></span> <span data-ttu-id="e573b-128">視電腦上 WCF 應用程式的執行時間特性而定，效能計數器記憶體可能會耗盡。</span><span class="sxs-lookup"><span data-stu-id="e573b-128">Depending upon the runtime characteristics of the WCF applications on a machine, performance counter memory may be exhausted.</span></span> <span data-ttu-id="e573b-129">發生這種情況時，WCF 會將錯誤寫入應用程式事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e573b-129">When this happens, WCF writes an error to the application event log.</span></span> <span data-ttu-id="e573b-130">錯誤的內容會說明效能計數器並未載入，且項目中會包含例外狀況「System.InvalidOperationException：自訂計數器檔案檢視記憶體不足」。</span><span class="sxs-lookup"><span data-stu-id="e573b-130">The content of the error states that a performance counter was not loaded, and the entry contains the exception "System.InvalidOperationException: Custom counters file view is out of memory."</span></span> <span data-ttu-id="e573b-131">如果已啟用錯誤層級的追蹤，則同樣會追蹤這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e573b-131">If tracing is enabled at the error level, this failure is also traced.</span></span> <span data-ttu-id="e573b-132">如果效能計數器記憶體用盡，繼續執行您的 WCF 應用程式並啟用效能計數器，可能會導致效能降低。</span><span class="sxs-lookup"><span data-stu-id="e573b-132">If performance counter memory is exhausted, continuing to run your WCF applications with performance counters enabled could result in performance degradation.</span></span> <span data-ttu-id="e573b-133">如果您是電腦的系統管理員，則應為電腦設定配置足夠的記憶體，支援可隨時存在的效能計數器數目上限。</span><span class="sxs-lookup"><span data-stu-id="e573b-133">If you are an administrator of the machine, you should configure it to allocate enough memory to support the maximum number of performance counters that can exist at any time.</span></span>  
  
 <span data-ttu-id="e573b-134">您可以在登錄中變更 WCF 類別的效能計數器記憶體量。</span><span class="sxs-lookup"><span data-stu-id="e573b-134">You can change the amount of performance counter memory for WCF categories in the registry.</span></span> <span data-ttu-id="e573b-135">若要執行這項操作，您必須將名為 `FileMappingSize` 的新 DWORD 值加入下列三個位置，並且將它設為所需的值 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="e573b-135">To do so, you need to add a new DWORD value named `FileMappingSize` to the three following locations, and set it to the desired value in bytes.</span></span> <span data-ttu-id="e573b-136">重新啟動您的電腦，讓這些變更生效。</span><span class="sxs-lookup"><span data-stu-id="e573b-136">Reboot your machine so that these changes are taken into effect.</span></span>  
  
- <span data-ttu-id="e573b-137">HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0\Performance</span><span class="sxs-lookup"><span data-stu-id="e573b-137">HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0\Performance</span></span>  
  
- <span data-ttu-id="e573b-138">HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0\Performance</span><span class="sxs-lookup"><span data-stu-id="e573b-138">HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0\Performance</span></span>  
  
- <span data-ttu-id="e573b-139">HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0\Performance</span><span class="sxs-lookup"><span data-stu-id="e573b-139">HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0\Performance</span></span>  
  
 <span data-ttu-id="e573b-140">處置掉大量物件 (例如 ServiceHost)，但在等待進行記憶體回收時，`PrivateBytes` 效能計數器將登錄相當大的數目。</span><span class="sxs-lookup"><span data-stu-id="e573b-140">When a large number of objects (for example, ServiceHost) are disposed of but waiting to be garbage-collected, the `PrivateBytes` performance counter will register an unusually high number.</span></span> <span data-ttu-id="e573b-141">若要解決這個問題，您可以加入自己的應用程式專屬計數器，或是使用 `performanceCounters` 屬性，僅啟用服務層級的計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-141">To resolve this problem, you can either add your own application-specific counters, or use the `performanceCounters` attribute to enable only service-level counters.</span></span>  
  
## <a name="types-of-performance-counters"></a><span data-ttu-id="e573b-142">效能計數器類型</span><span class="sxs-lookup"><span data-stu-id="e573b-142">Types of Performance Counters</span></span>  
 <span data-ttu-id="e573b-143">效能計數器分成三種不同的層級：服務、端點和作業。</span><span class="sxs-lookup"><span data-stu-id="e573b-143">Performance counters are scoped to three different levels: Service, Endpoint and Operation.</span></span>  
  
 <span data-ttu-id="e573b-144">您可以使用 WMI 擷取效能計數器執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="e573b-144">You can use WMI to retrieve the name of a performance counter instance.</span></span> <span data-ttu-id="e573b-145">例如，</span><span class="sxs-lookup"><span data-stu-id="e573b-145">For example,</span></span>  
  
- <span data-ttu-id="e573b-146">您可以透過 WMI [服務](../wmi/service.md) 實例的 "CounterInstanceName" 屬性取得服務計數器實例名稱。</span><span class="sxs-lookup"><span data-stu-id="e573b-146">Service counter instance name can be obtained through WMI [Service](../wmi/service.md) instance's "CounterInstanceName" property.</span></span>  
  
- <span data-ttu-id="e573b-147">端點計數器實例名稱可透過 WMI [端點](../wmi/endpoint.md) 實例的 "CounterInstanceName" 屬性取得。</span><span class="sxs-lookup"><span data-stu-id="e573b-147">Endpoint counter instance name can be obtained through WMI [Endpoint](../wmi/endpoint.md) instance's "CounterInstanceName" property.</span></span>  
  
- <span data-ttu-id="e573b-148">您可以透過 WMI [端點](../wmi/endpoint.md) 實例的 "GetOperationCounterInstanceName" 方法取得作業計數器實例名稱。</span><span class="sxs-lookup"><span data-stu-id="e573b-148">Operation counter instance name can be obtained through WMI [Endpoint](../wmi/endpoint.md) instance's "GetOperationCounterInstanceName" method.</span></span>  
  
 <span data-ttu-id="e573b-149">如需 WMI 的詳細資訊，請參閱 [使用 Windows Management Instrumentation 進行診斷](../wmi/index.md)。</span><span class="sxs-lookup"><span data-stu-id="e573b-149">For more information on WMI, see [Using Windows Management Instrumentation for Diagnostics](../wmi/index.md).</span></span>  
  
### <a name="service-performance-counters"></a><span data-ttu-id="e573b-150">服務效能計數器</span><span class="sxs-lookup"><span data-stu-id="e573b-150">Service performance counters</span></span>  
 <span data-ttu-id="e573b-151">服務效能計數器會測量整體的服務行為，而且可用於診斷整個服務的效能。</span><span class="sxs-lookup"><span data-stu-id="e573b-151">Service performance counters measure the service behavior as a whole and can be used to diagnose the performance of the whole service.</span></span> <span data-ttu-id="e573b-152">以效能監視器進行檢視時，可以在 `ServiceModelService 4.0.0.0` 效能物件下找到它們。</span><span class="sxs-lookup"><span data-stu-id="e573b-152">They can be found under the `ServiceModelService 4.0.0.0` performance object when viewing with Performance Monitor.</span></span> <span data-ttu-id="e573b-153">執行個體會使用以下模式來命名：</span><span class="sxs-lookup"><span data-stu-id="e573b-153">The instances are named using the following pattern:</span></span>  
  
`ServiceName@ServiceBaseAddress`
  
 <span data-ttu-id="e573b-154">服務範圍中之計數器是從端點集合中的計數器彙總而來的。</span><span class="sxs-lookup"><span data-stu-id="e573b-154">A counter in a service scope is aggregated from counter in a collection of endpoints.</span></span>  
  
 <span data-ttu-id="e573b-155">當建立新的 InstanceContext 時，會遞增服務執行個體建立的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-155">Performance counters for service instance creation are incremented when a new InstanceContext is created.</span></span> <span data-ttu-id="e573b-156">請注意，即使您收到不停用訊息 (現有服務)，或者您從一個工作階段連接到執行個體、結束執行個體，然後再重新從另一個執行個體連線，都還是會建立新的 InstanceContext。</span><span class="sxs-lookup"><span data-stu-id="e573b-156">Note that a new InstanceContext is created even when you receive a non-activating message (with an existing service), or when you connect to an instance from one session, end the session, and then reconnect from another session.</span></span>  
  
### <a name="endpoint-performance-counters"></a><span data-ttu-id="e573b-157">端點效能計數器</span><span class="sxs-lookup"><span data-stu-id="e573b-157">Endpoint performance counters</span></span>  
 <span data-ttu-id="e573b-158">您以端點效能計數器查看的資料，反映了端點接受訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="e573b-158">Endpoint performance counters enable you to look at data reflecting how an endpoint is accepting messages.</span></span> <span data-ttu-id="e573b-159">使用效能監視器進行檢視時，可以在 `ServiceModelEndpoint 4.0.0.0` 效能物件下找到它們。</span><span class="sxs-lookup"><span data-stu-id="e573b-159">They can be found under the `ServiceModelEndpoint 4.0.0.0` performance object when viewing using the Performance Monitor.</span></span> <span data-ttu-id="e573b-160">執行個體會使用以下模式來命名：</span><span class="sxs-lookup"><span data-stu-id="e573b-160">The instances are named using the following pattern:</span></span>  
  
`(ServiceName).(ContractName)@(endpoint listener address)`
  
 <span data-ttu-id="e573b-161">這些資料與針對個別作業所收集的資料類似，但是只會彙總端點之間的資料。</span><span class="sxs-lookup"><span data-stu-id="e573b-161">The data is similar to what is collected for individual operations, but is only aggregated across the endpoint.</span></span>  
  
 <span data-ttu-id="e573b-162">端點範圍中的計數器是從作業集合中的計數器彙總而來的。</span><span class="sxs-lookup"><span data-stu-id="e573b-162">A counter in an endpoint scope is aggregated from counters in a collection of operations.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e573b-163">如果兩個端點擁有相同的合約名稱和位址，則它們都會對應到相同的計數器執行個體。</span><span class="sxs-lookup"><span data-stu-id="e573b-163">If two endpoints have identical contract names and addresses, they are mapped to the same counter instance.</span></span>  
  
### <a name="operation-performance-counters"></a><span data-ttu-id="e573b-164">作業效能計數器</span><span class="sxs-lookup"><span data-stu-id="e573b-164">Operation performance counters</span></span>  
 <span data-ttu-id="e573b-165">當使用效能監視器進行檢視時，您可以在 `ServiceModelOperation 4.0.0.0` 效能物件中找到作業效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-165">Operation performance counters are found under the `ServiceModelOperation 4.0.0.0` performance object when viewing with the Performance Monitor.</span></span> <span data-ttu-id="e573b-166">每個作業都有個別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="e573b-166">Each operation has an individual instance.</span></span> <span data-ttu-id="e573b-167">也就是，如果指定的合約有 10 個作業，就會有 10 個作業計數器執行個體與該合約產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e573b-167">That is, if a given contract has 10 operations, 10 operation counter instances are associated with that contract.</span></span> <span data-ttu-id="e573b-168">物件執行個體會使用以下模式來命名：</span><span class="sxs-lookup"><span data-stu-id="e573b-168">The object instances are named using the following pattern:</span></span>  
  
`(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)`
  
 <span data-ttu-id="e573b-169">這個計數器能夠讓您測量呼叫的使用狀況，以及作業的執行效能。</span><span class="sxs-lookup"><span data-stu-id="e573b-169">This counter enables you to measure how the call is being used and how well the operation is performing.</span></span>  
  
 <span data-ttu-id="e573b-170">如果可在多個範圍內看見此類計數器，則從較高範圍所收集的資料會與來自較低範圍的資料進行彙總。</span><span class="sxs-lookup"><span data-stu-id="e573b-170">When counters are visible at multiple scopes, data gathered from a higher scope are aggregated with data from lower scopes.</span></span> <span data-ttu-id="e573b-171">例如，在端點的 `Calls` 代表該端點內所有作業呼叫的加總，而在服務中的 `Calls`，則代表服務內所有端點之所有呼叫的加總。</span><span class="sxs-lookup"><span data-stu-id="e573b-171">For example, `Calls` at an endpoint represents the sum of all operation calls within the endpoint; `Calls` at a service represents the sum of all calls to all endpoints within the service.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e573b-172">如果您的合約上有重複的作業名稱，則這兩個作業只能取得一個計數器執行個體。</span><span class="sxs-lookup"><span data-stu-id="e573b-172">If you have duplicate operation names on a contract, you only get one counter instances for both operations.</span></span>  
  
## <a name="programming-the-wcf-performance-counters"></a><span data-ttu-id="e573b-173">WCF 效能計數器程式設計</span><span class="sxs-lookup"><span data-stu-id="e573b-173">Programming the WCF Performance Counters</span></span>  

<span data-ttu-id="e573b-174">SDK 安裝資料夾中安裝了數個檔案，因此您可以透過程式設計的方式存取 WCF 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e573b-174">Several files are installed in the SDK install folder so that you can access the WCF performance counters programmatically.</span></span> <span data-ttu-id="e573b-175">這些檔案列示如下：</span><span class="sxs-lookup"><span data-stu-id="e573b-175">These files are listed as follows:</span></span>
  
- <span data-ttu-id="e573b-176">*\_ServiceModelEndpointPerfCounters.vrg*</span><span class="sxs-lookup"><span data-stu-id="e573b-176">*\_ServiceModelEndpointPerfCounters.vrg*</span></span>
- <span data-ttu-id="e573b-177">*\_ServiceModelOperationPerfCounters.vrg*</span><span class="sxs-lookup"><span data-stu-id="e573b-177">*\_ServiceModelOperationPerfCounters.vrg*</span></span>
- <span data-ttu-id="e573b-178">*\_ServiceModelServicePerfCounters.vrg*</span><span class="sxs-lookup"><span data-stu-id="e573b-178">*\_ServiceModelServicePerfCounters.vrg*</span></span>  
- <span data-ttu-id="e573b-179">*\_SMSvcHostPerfCounters.vrg*</span><span class="sxs-lookup"><span data-stu-id="e573b-179">*\_SMSvcHostPerfCounters.vrg*</span></span>
- <span data-ttu-id="e573b-180">*\_TransactionBridgePerfCounters.vrg*</span><span class="sxs-lookup"><span data-stu-id="e573b-180">*\_TransactionBridgePerfCounters.vrg*</span></span>
  
<span data-ttu-id="e573b-181">如需如何以程式設計方式存取計數器的詳細資訊，請參閱 [效能計數器程式設計架構](/previous-versions/visualstudio/visual-studio-2008/5f9bkxzf(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="e573b-181">For more information on how to access the counters programmatically, see [Performance Counter Programming Architecture](/previous-versions/visualstudio/visual-studio-2008/5f9bkxzf(v=vs.90)).</span></span>
  
## <a name="see-also"></a><span data-ttu-id="e573b-182">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e573b-182">See also</span></span>

- [<span data-ttu-id="e573b-183">系統管理與診斷</span><span class="sxs-lookup"><span data-stu-id="e573b-183">Administration and Diagnostics</span></span>](../index.md)
