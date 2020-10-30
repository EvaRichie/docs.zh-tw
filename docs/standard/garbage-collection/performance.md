---
title: 記憶體回收和效能
description: 瞭解垃圾收集和記憶體使用量的相關問題。 瞭解如何將垃圾收集對應用程式的影響降至最低。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, troubleshooting
- garbage collection, performance
ms.assetid: c203467b-e95c-4ccf-b30b-953eb3463134
ms.openlocfilehash: 7c4a61c1e5e735313a355bcab348fd6ef58a8686
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2020
ms.locfileid: "93062967"
---
# <a name="garbage-collection-and-performance"></a><span data-ttu-id="6a72c-104">記憶體回收和效能</span><span class="sxs-lookup"><span data-stu-id="6a72c-104">Garbage Collection and Performance</span></span>

<span data-ttu-id="6a72c-105">本主題描述記憶體回收和記憶體使用量的相關問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-105">This topic describes issues related to garbage collection and memory usage.</span></span> <span data-ttu-id="6a72c-106">它解決關於 Managed 堆積的問題，並說明如何將記憶體回收對應用程式的影響降至最低。</span><span class="sxs-lookup"><span data-stu-id="6a72c-106">It addresses issues that pertain to the managed heap and explains how to minimize the effect of garbage collection on your applications.</span></span> <span data-ttu-id="6a72c-107">每個問題已連結至程序，可讓您用來調查問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-107">Each issue has links to procedures that you can use to investigate problems.</span></span>

## <a name="performance-analysis-tools"></a><span data-ttu-id="6a72c-108">效能分析工具</span><span class="sxs-lookup"><span data-stu-id="6a72c-108">Performance Analysis Tools</span></span>

<span data-ttu-id="6a72c-109">下列各節說明可用來調查記憶體使用量和記憶體回收問題的工具。</span><span class="sxs-lookup"><span data-stu-id="6a72c-109">The following sections describe the tools that are available for investigating memory usage and garbage collection issues.</span></span> <span data-ttu-id="6a72c-110">本主題稍後提供的[程序](#performance-check-procedures)會參考這些工具。</span><span class="sxs-lookup"><span data-stu-id="6a72c-110">The [procedures](#performance-check-procedures) provided later in this topic refer to these tools.</span></span>

### <a name="memory-performance-counters"></a><span data-ttu-id="6a72c-111">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="6a72c-111">Memory Performance Counters</span></span>

<span data-ttu-id="6a72c-112">您可以使用效能計數器來收集效能資料。</span><span class="sxs-lookup"><span data-stu-id="6a72c-112">You can use performance counters to gather performance data.</span></span> <span data-ttu-id="6a72c-113">如需相關指示，請參閱[執行階段分析](../../framework/debug-trace-profile/runtime-profiling.md)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-113">For instructions, see [Runtime Profiling](../../framework/debug-trace-profile/runtime-profiling.md).</span></span> <span data-ttu-id="6a72c-114">效能計數器的 .NET CLR 記憶體類別，如 [.net 中的效能計數器](../../framework/debug-trace-profile/performance-counters.md)所述，會提供垃圾收集行程的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6a72c-114">The .NET CLR Memory category of performance counters, as described in [Performance Counters in .NET](../../framework/debug-trace-profile/performance-counters.md), provides information about the garbage collector.</span></span>

### <a name="debugging-with-sos"></a><span data-ttu-id="6a72c-115">以 SOS 偵錯</span><span class="sxs-lookup"><span data-stu-id="6a72c-115">Debugging with SOS</span></span>

<span data-ttu-id="6a72c-116">您可以使用 [Windows 偵錯工具 (WinDbg)](/windows-hardware/drivers/debugger/index) 來檢查 Managed 堆積上的物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-116">You can use the [Windows Debugger (WinDbg)](/windows-hardware/drivers/debugger/index) to inspect objects on the managed heap.</span></span>

<span data-ttu-id="6a72c-117">若要安裝 WinDbg，請從[下載 Debugging Tools for Windows](/windows-hardware/drivers/debugger/debugger-download-tools) 頁面安裝 Debugging Tools for Windows。</span><span class="sxs-lookup"><span data-stu-id="6a72c-117">To install WinDbg, install Debugging Tools for Windows from the [Download Debugging Tools for Windows](/windows-hardware/drivers/debugger/debugger-download-tools) page.</span></span>

### <a name="garbage-collection-etw-events"></a><span data-ttu-id="6a72c-118">記憶體回收 ETW 事件</span><span class="sxs-lookup"><span data-stu-id="6a72c-118">Garbage Collection ETW Events</span></span>

<span data-ttu-id="6a72c-119">Windows 事件追蹤 (ETW) 是一種追蹤系統，可補充 .NET 所提供的程式碼剖析和偵錯工具支援。</span><span class="sxs-lookup"><span data-stu-id="6a72c-119">Event tracing for Windows (ETW) is a tracing system that supplements the profiling and debugging support provided by .NET.</span></span> <span data-ttu-id="6a72c-120">從 .NET Framework 4 開始， [垃圾收集 ETW 事件](../../framework/performance/garbage-collection-etw-events.md) 會捕捉實用的資訊，以便從統計的觀點來分析 managed 堆積。</span><span class="sxs-lookup"><span data-stu-id="6a72c-120">Starting with .NET Framework 4, [garbage collection ETW events](../../framework/performance/garbage-collection-etw-events.md) capture useful information for analyzing the managed heap from a statistical point of view.</span></span> <span data-ttu-id="6a72c-121">例如，引發 `GCStart_V1` 事件時，會發生記憶體回收，這會提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="6a72c-121">For example, the `GCStart_V1` event, which is raised when a garbage collection is about to occur, provides the following information:</span></span>

- <span data-ttu-id="6a72c-122">所收集物件的層代。</span><span class="sxs-lookup"><span data-stu-id="6a72c-122">Which generation of objects is being collected.</span></span>

- <span data-ttu-id="6a72c-123">觸發記憶體回收的原因。</span><span class="sxs-lookup"><span data-stu-id="6a72c-123">What triggered the garbage collection.</span></span>

- <span data-ttu-id="6a72c-124">記憶體回收 (並行或不同時) 的類型。</span><span class="sxs-lookup"><span data-stu-id="6a72c-124">Type of garbage collection (concurrent or not concurrent).</span></span>

<span data-ttu-id="6a72c-125">ETW 事件記錄很有效率，且不會遮蓋與記憶體回收相關聯的任何效能問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-125">ETW event logging is efficient and will not mask any performance problems associated with garbage collection.</span></span> <span data-ttu-id="6a72c-126">處理程序可以提供自己的事件來搭配 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-126">A process can provide its own events in conjunction with ETW events.</span></span> <span data-ttu-id="6a72c-127">記錄時，應用程式的事件和記憶體回收事件都可以相互關聯，以判斷堆積問題發生的方式和時間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-127">When logged, both the application's events and the garbage collection events can be correlated to determine how and when heap problems occur.</span></span> <span data-ttu-id="6a72c-128">例如，伺服器應用程式可以在用戶端要求開始和結束時提供事件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-128">For example, a server application could provide events at the start and end of a client request.</span></span>

### <a name="the-profiling-api"></a><span data-ttu-id="6a72c-129">程式碼剖析 API</span><span class="sxs-lookup"><span data-stu-id="6a72c-129">The Profiling API</span></span>

<span data-ttu-id="6a72c-130">Common Language Runtime (CLR) 程式碼剖析介面提供在記憶體回收期間受影響之物件的詳細相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6a72c-130">The common language runtime (CLR) profiling interfaces provide detailed information about the objects that were affected during garbage collection.</span></span> <span data-ttu-id="6a72c-131">當記憶體回收開始和結束時，會通知程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="6a72c-131">A profiler can be notified when a garbage collection starts and ends.</span></span> <span data-ttu-id="6a72c-132">它可以提供 Managed 堆積上之物件的相關報告，包括每個層代中的物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="6a72c-132">It can provide reports about the objects on the managed heap, including an identification of objects in each generation.</span></span> <span data-ttu-id="6a72c-133">如需詳細資訊，請參閱[分析概觀](../../framework/unmanaged-api/profiling/profiling-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-133">For more information, see [Profiling Overview](../../framework/unmanaged-api/profiling/profiling-overview.md).</span></span>

<span data-ttu-id="6a72c-134">程式碼剖析工具可以提供完整的資訊。</span><span class="sxs-lookup"><span data-stu-id="6a72c-134">Profilers can provide comprehensive information.</span></span> <span data-ttu-id="6a72c-135">不過，複雜的程式碼剖析工具可能會修改應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="6a72c-135">However, complex profilers can potentially modify an application's behavior.</span></span>

### <a name="application-domain-resource-monitoring"></a><span data-ttu-id="6a72c-136">應用程式定義域資源監視</span><span class="sxs-lookup"><span data-stu-id="6a72c-136">Application Domain Resource Monitoring</span></span>

<span data-ttu-id="6a72c-137">從 .NET Framework 4 開始， (ARM) 的應用程式域資源監視可讓主機監視應用程式域的 CPU 和記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-137">Starting with .NET Framework 4, Application domain resource monitoring (ARM) enables hosts to monitor CPU and memory usage by application domain.</span></span> <span data-ttu-id="6a72c-138">如需詳細資訊，請參閱[應用程式定義域資源監視](app-domain-resource-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-138">For more information, see [Application Domain Resource Monitoring](app-domain-resource-monitoring.md).</span></span>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="6a72c-139">效能問題疑難排解</span><span class="sxs-lookup"><span data-stu-id="6a72c-139">Troubleshooting Performance Issues</span></span>

<span data-ttu-id="6a72c-140">第一個步驟是[判斷問題是否真的是記憶體回收](#IsGC)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-140">The first step is to [determine whether the issue is actually garbage collection](#IsGC).</span></span> <span data-ttu-id="6a72c-141">如果您判斷是，則請從下列清單選取以疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-141">If you determine that it is, select from the following list to troubleshoot the problem.</span></span>

- [<span data-ttu-id="6a72c-142">擲回記憶體不足例外狀況</span><span class="sxs-lookup"><span data-stu-id="6a72c-142">An out-of-memory exception is thrown</span></span>](#Issue_OOM)

- [<span data-ttu-id="6a72c-143">處理序使用太多記憶體</span><span class="sxs-lookup"><span data-stu-id="6a72c-143">The process uses too much memory</span></span>](#Issue_TooMuchMemory)

- [<span data-ttu-id="6a72c-144">記憶體回收行程回收物件速度不夠快</span><span class="sxs-lookup"><span data-stu-id="6a72c-144">The garbage collector does not reclaim objects fast enough</span></span>](#Issue_NotFastEnough)

- [<span data-ttu-id="6a72c-145">Managed 堆積太過分散</span><span class="sxs-lookup"><span data-stu-id="6a72c-145">The managed heap is too fragmented</span></span>](#Issue_Fragmentation)

- [<span data-ttu-id="6a72c-146">記憶體回收暫停太長</span><span class="sxs-lookup"><span data-stu-id="6a72c-146">Garbage collection pauses are too long</span></span>](#Issue_LongPauses)

- [<span data-ttu-id="6a72c-147">層代 0 太大</span><span class="sxs-lookup"><span data-stu-id="6a72c-147">Generation 0 is too big</span></span>](#Issue_Gen0)

- [<span data-ttu-id="6a72c-148">在記憶體回收期間的 CPU 使用量太高</span><span class="sxs-lookup"><span data-stu-id="6a72c-148">CPU usage during a garbage collection is too high</span></span>](#Issue_HighCPU)

<a name="Issue_OOM"></a>

### <a name="issue-an-out-of-memory-exception-is-thrown"></a><span data-ttu-id="6a72c-149">問題：擲回記憶體不足例外狀況</span><span class="sxs-lookup"><span data-stu-id="6a72c-149">Issue: An Out-of-Memory Exception Is Thrown</span></span>

<span data-ttu-id="6a72c-150">有兩種合理狀況會擲回 Managed <xref:System.OutOfMemoryException>：</span><span class="sxs-lookup"><span data-stu-id="6a72c-150">There are two legitimate cases for a managed <xref:System.OutOfMemoryException> to be thrown:</span></span>

- <span data-ttu-id="6a72c-151">虛擬記憶體不足。</span><span class="sxs-lookup"><span data-stu-id="6a72c-151">Running out of virtual memory.</span></span>

  <span data-ttu-id="6a72c-152">記憶體回收行程會以預先決定大小的區段，從系統配置記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-152">The garbage collector allocates memory from the system in segments of a pre-determined size.</span></span> <span data-ttu-id="6a72c-153">如果配置需要額外的區段，但處理序的虛擬記憶體空間中沒有剩下連續的可用區塊，則 Managed 堆積配置將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6a72c-153">If an allocation requires an additional segment, but there is no contiguous free block left in the process's virtual memory space, the allocation for the managed heap will fail.</span></span>

- <span data-ttu-id="6a72c-154">沒有足夠的實體記憶體可配置。</span><span class="sxs-lookup"><span data-stu-id="6a72c-154">Not having enough physical memory to allocate.</span></span>

|<span data-ttu-id="6a72c-155">效能檢查</span><span class="sxs-lookup"><span data-stu-id="6a72c-155">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="6a72c-156">判斷記憶體不足例外狀況是否為 Managed。</span><span class="sxs-lookup"><span data-stu-id="6a72c-156">Determine whether the out-of-memory exception is managed.</span></span>](#OOMIsManaged)<br /><br /> [<span data-ttu-id="6a72c-157">判斷可以保留多少虛擬記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-157">Determine how much virtual memory can be reserved.</span></span>](#GetVM)<br /><br /> [<span data-ttu-id="6a72c-158">判斷是否有足夠的實體記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-158">Determine whether there is enough physical memory.</span></span>](#Physical)|

<span data-ttu-id="6a72c-159">如果您判斷例外狀況不合法，請連絡 Microsoft 客戶服務及支援，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="6a72c-159">If you determine that the exception is not legitimate, contact Microsoft Customer Service and Support with the following information:</span></span>

- <span data-ttu-id="6a72c-160">具有受管理的記憶體不足例外狀況的堆疊。</span><span class="sxs-lookup"><span data-stu-id="6a72c-160">The stack with the managed out-of-memory exception.</span></span>

- <span data-ttu-id="6a72c-161">完整記憶體傾印。</span><span class="sxs-lookup"><span data-stu-id="6a72c-161">Full memory dump.</span></span>

- <span data-ttu-id="6a72c-162">證明它是不合法的記憶體不足例外狀況的資料，包括顯示虛擬或實體記憶體不是問題的資料。</span><span class="sxs-lookup"><span data-stu-id="6a72c-162">Data that proves that it is not a legitimate out-of-memory exception, including data that shows that virtual or physical memory is not an issue.</span></span>

<a name="Issue_TooMuchMemory"></a>

### <a name="issue-the-process-uses-too-much-memory"></a><span data-ttu-id="6a72c-163">問題：處理序使用太多記憶體</span><span class="sxs-lookup"><span data-stu-id="6a72c-163">Issue: The Process Uses Too Much Memory</span></span>

<span data-ttu-id="6a72c-164">常見的假設是 Windows 工作管理員 [效能]  索引標籤上的記憶體使用量顯示可以指出使用太多記憶體的時刻。</span><span class="sxs-lookup"><span data-stu-id="6a72c-164">A common assumption is that the memory usage display on the **Performance** tab of Windows Task Manager can indicate when too much memory is being used.</span></span> <span data-ttu-id="6a72c-165">不過，該顯示與工作集有關；它不提供虛擬記憶體使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6a72c-165">However, that display pertains to the working set; it does not provide information about virtual memory usage.</span></span>

<span data-ttu-id="6a72c-166">如果您判斷問題是 Managed 堆積所導致，您必須在一段時間內測量 Managed 堆積，以判斷任何模式。</span><span class="sxs-lookup"><span data-stu-id="6a72c-166">If you determine that the issue is caused by the managed heap, you must measure the managed heap over time to determine any patterns.</span></span>

<span data-ttu-id="6a72c-167">如果您判斷問題不是 Managed 堆積所導致，則您必須使用原生偵錯。</span><span class="sxs-lookup"><span data-stu-id="6a72c-167">If you determine that the problem is not caused by the managed heap, you must use native debugging.</span></span>

|<span data-ttu-id="6a72c-168">效能檢查</span><span class="sxs-lookup"><span data-stu-id="6a72c-168">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="6a72c-169">判斷可以保留多少虛擬記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-169">Determine how much virtual memory can be reserved.</span></span>](#GetVM)<br /><br /> [<span data-ttu-id="6a72c-170">判斷 Managed 堆積正在認可的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-170">Determine how much memory the managed heap is committing.</span></span>](#ManagedHeapCommit)<br /><br /> [<span data-ttu-id="6a72c-171">判斷 Managed 堆積保留的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-171">Determine how much memory the managed heap reserves.</span></span>](#ManagedHeapReserve)<br /><br /> [<span data-ttu-id="6a72c-172">判斷層代 2 的大型物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-172">Determine large objects in generation 2.</span></span>](#ExamineGen2)<br /><br /> [<span data-ttu-id="6a72c-173">判斷物件的參考。</span><span class="sxs-lookup"><span data-stu-id="6a72c-173">Determine references to objects.</span></span>](#ObjRef)|

<a name="Issue_NotFastEnough"></a>

### <a name="issue-the-garbage-collector-does-not-reclaim-objects-fast-enough"></a><span data-ttu-id="6a72c-174">問題：記憶體回收行程回收物件速度不夠快</span><span class="sxs-lookup"><span data-stu-id="6a72c-174">Issue: The Garbage Collector Does Not Reclaim Objects Fast Enough</span></span>

<span data-ttu-id="6a72c-175">當物件似乎未如預期般被回收以進行記憶體回收時，您必須判斷是否有對這些物件的任何強式參考。</span><span class="sxs-lookup"><span data-stu-id="6a72c-175">When it appears as if objects are not being reclaimed as expected for garbage collection, you must determine if there are any strong references to those objects.</span></span>

<span data-ttu-id="6a72c-176">如果包含無作用物件的層代已經沒有記憶體回收 (表示尚未執行無作用物件的完成項)，您也可能會遇到這個問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-176">You may also encounter this issue if there has been no garbage collection for the generation that contains a dead object, which indicates that the finalizer for the dead object has not been run.</span></span> <span data-ttu-id="6a72c-177">比方說，這可能發生在您執行單一執行緒 Apartment (STA) 應用程式和服務完成項佇列的執行緒無法呼叫到它時。</span><span class="sxs-lookup"><span data-stu-id="6a72c-177">For example, this is possible when you are running a single-threaded apartment (STA) application and the thread that services the finalizer queue cannot call into it.</span></span>

|<span data-ttu-id="6a72c-178">效能檢查</span><span class="sxs-lookup"><span data-stu-id="6a72c-178">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="6a72c-179">檢查物件的參考。</span><span class="sxs-lookup"><span data-stu-id="6a72c-179">Check references to objects.</span></span>](#ObjRef)<br /><br /> [<span data-ttu-id="6a72c-180">判斷是否已執行完成項。</span><span class="sxs-lookup"><span data-stu-id="6a72c-180">Determine whether a finalizer has been run.</span></span>](#Induce)<br /><br /> [<span data-ttu-id="6a72c-181">判斷是否有等候完成的物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-181">Determine whether there are objects waiting to be finalized.</span></span>](#Finalize)|

<a name="Issue_Fragmentation"></a>

### <a name="issue-the-managed-heap-is-too-fragmented"></a><span data-ttu-id="6a72c-182">問題：Managed 堆積太過分散</span><span class="sxs-lookup"><span data-stu-id="6a72c-182">Issue: The Managed Heap Is Too fragmented</span></span>

<span data-ttu-id="6a72c-183">分散層級的計算方式是可用空間佔層代配置記憶體總數的比例。</span><span class="sxs-lookup"><span data-stu-id="6a72c-183">The fragmentation level is calculated as the ratio of free space over the total allocated memory for the generation.</span></span> <span data-ttu-id="6a72c-184">針對層代 2，可接受的分散層級是不超過 20%。</span><span class="sxs-lookup"><span data-stu-id="6a72c-184">For generation 2, an acceptable level of fragmentation is no more than 20%.</span></span> <span data-ttu-id="6a72c-185">層代 2 可能會非常大，因此分散比例比絕對值更重要。</span><span class="sxs-lookup"><span data-stu-id="6a72c-185">Because generation 2 can get very big, the ratio of fragmentation is more important than the absolute value.</span></span>

<span data-ttu-id="6a72c-186">層代 0 中有很多可用空間不成問題，因為這是配置新物件配置所在的層代。</span><span class="sxs-lookup"><span data-stu-id="6a72c-186">Having lots of free space in generation 0 is not a problem because this is the generation where new objects are allocated.</span></span>

<span data-ttu-id="6a72c-187">分散一律發生在大型物件堆積中，因為它不會壓縮。</span><span class="sxs-lookup"><span data-stu-id="6a72c-187">Fragmentation always occurs in the large object heap because it is not compacted.</span></span> <span data-ttu-id="6a72c-188">相鄰的可用物件自然而然會聚攏成為單一空間，以滿足大型物件配置要求。</span><span class="sxs-lookup"><span data-stu-id="6a72c-188">Free objects that are adjacent are naturally collapsed into a single space to satisfy large object allocation requests.</span></span>

<span data-ttu-id="6a72c-189">分散可能會在層代 1 和層代 2 成為問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-189">Fragmentation can become a problem in generation 1 and generation 2.</span></span> <span data-ttu-id="6a72c-190">如果這些層代在記憶體回收之後有大量的可用空間，應用程式的物件使用方式可能需要修改，而且您應該考慮重新評估長期物件的存留期。</span><span class="sxs-lookup"><span data-stu-id="6a72c-190">If these generations have a large amount of free space after a garbage collection, an application's object usage may need modification, and you should consider re-evaluating the lifetime of long-term objects.</span></span>

<span data-ttu-id="6a72c-191">固定過多物件可能會增加分散。</span><span class="sxs-lookup"><span data-stu-id="6a72c-191">Excessive pinning of objects can increase fragmentation.</span></span> <span data-ttu-id="6a72c-192">如果片段很高，則可能已釘選過多物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-192">If fragmentation is high, too many objects could have been pinned.</span></span>

<span data-ttu-id="6a72c-193">如果虛擬記憶體的分散導致記憶體回收行程無法加入區段，原因可能是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="6a72c-193">If fragmentation of virtual memory is preventing the garbage collector from adding segments, the causes could be one of the following:</span></span>

- <span data-ttu-id="6a72c-194">經常載入及卸載許多小型組件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-194">Frequent loading and unloading of many small assemblies.</span></span>

- <span data-ttu-id="6a72c-195">與 Unmanaged 程式碼交互作用時，保留太多 COM 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="6a72c-195">Holding too many references to COM objects when interoperating with unmanaged code.</span></span>

- <span data-ttu-id="6a72c-196">建立大型的暫時性物件，這會造成大型物件堆積頻繁地配置和釋放堆積區段。</span><span class="sxs-lookup"><span data-stu-id="6a72c-196">Creation of large transient objects, which causes the large object heap to allocate and free heap segments frequently.</span></span>

  <span data-ttu-id="6a72c-197">裝載 CLR 時，應用程式可以要求記憶體回收行程保留其區段。</span><span class="sxs-lookup"><span data-stu-id="6a72c-197">When hosting the CLR, an application can request that the garbage collector retain its segments.</span></span> <span data-ttu-id="6a72c-198">這會減少區段配置的頻率。</span><span class="sxs-lookup"><span data-stu-id="6a72c-198">This reduces the frequency of segment allocations.</span></span> <span data-ttu-id="6a72c-199">這可以藉由使用 [STARTUP_FLAGS 列舉](../../framework/unmanaged-api/hosting/startup-flags-enumeration.md)中的 STARTUP_HOARD_GC_VM 旗標來達成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-199">This is accomplished by using the STARTUP_HOARD_GC_VM flag in the [STARTUP_FLAGS Enumeration](../../framework/unmanaged-api/hosting/startup-flags-enumeration.md).</span></span>

|<span data-ttu-id="6a72c-200">效能檢查</span><span class="sxs-lookup"><span data-stu-id="6a72c-200">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="6a72c-201">判斷 Managed 堆積中的可用空間數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-201">Determine the amount of free space in the managed heap.</span></span>](#Fragmented)<br /><br /> [<span data-ttu-id="6a72c-202">判斷被固定的物件數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-202">Determine the number of pinned objects.</span></span>](#Pinned)|

<span data-ttu-id="6a72c-203">如果您認為是不合法的分散原因，請連絡 Microsoft 客戶服務及支援中心。</span><span class="sxs-lookup"><span data-stu-id="6a72c-203">If you think that there is no legitimate cause for the fragmentation, contact Microsoft Customer Service and Support.</span></span>

<a name="Issue_LongPauses"></a>

### <a name="issue-garbage-collection-pauses-are-too-long"></a><span data-ttu-id="6a72c-204">問題：記憶體回收暫停太長</span><span class="sxs-lookup"><span data-stu-id="6a72c-204">Issue: Garbage Collection Pauses Are Too Long</span></span>

<span data-ttu-id="6a72c-205">記憶體回收以軟性即時方式運作，所以應用程式必須能夠容忍某些暫停。</span><span class="sxs-lookup"><span data-stu-id="6a72c-205">Garbage collection operates in soft real time, so an application must be able to tolerate some pauses.</span></span> <span data-ttu-id="6a72c-206">軟性即時的準則是 95% 的作業必須準時完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-206">A criterion for soft real time is that 95% of the operations must finish on time.</span></span>

<span data-ttu-id="6a72c-207">在並行記憶體回收中，Managed 執行緒可以在回收期間執行，這表示很少暫停。</span><span class="sxs-lookup"><span data-stu-id="6a72c-207">In concurrent garbage collection, managed threads are allowed to run during a collection, which means that pauses are very minimal.</span></span>

<span data-ttu-id="6a72c-208">暫時記憶體回收 (層代 0 和 1) 只會持續幾毫秒，因此減少暫停通常並不可行。</span><span class="sxs-lookup"><span data-stu-id="6a72c-208">Ephemeral garbage collections (generations 0 and 1) last only a few milliseconds, so decreasing pauses is usually not feasible.</span></span> <span data-ttu-id="6a72c-209">不過，您可以變更應用程式的配置要求模式，來減少在層代 2 回收中的暫停。</span><span class="sxs-lookup"><span data-stu-id="6a72c-209">However, you can decrease the pauses in generation 2 collections by changing the pattern of allocation requests by an application.</span></span>

<span data-ttu-id="6a72c-210">另一個、更正確的方法是使用[記憶體回收 ETW 事件](../../framework/performance/garbage-collection-etw-events.md)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-210">Another, more accurate, method is to use [garbage collection ETW events](../../framework/performance/garbage-collection-etw-events.md).</span></span> <span data-ttu-id="6a72c-211">您可以藉由加入一系列事件的時間戳記差異來尋找回收的時機。</span><span class="sxs-lookup"><span data-stu-id="6a72c-211">You can find the timings for collections by adding the time stamp differences for a sequence of events.</span></span> <span data-ttu-id="6a72c-212">整個回收順序包含擱置執行引擎、記憶體回收本身，以及繼續執行引擎。</span><span class="sxs-lookup"><span data-stu-id="6a72c-212">The whole collection sequence includes suspension of the execution engine, the garbage collection itself, and the resumption of the execution engine.</span></span>

<span data-ttu-id="6a72c-213">您可以使用[記憶體回收通知](notifications.md)判斷伺服器是否即將有層代 2 回收，及將要求重設路徑到另一部伺服器是否可以緩解任何暫停問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-213">You can use [Garbage Collection Notifications](notifications.md) to determine whether a server is about to have a generation 2 collection, and whether rerouting requests to another server could ease any problems with pauses.</span></span>

|<span data-ttu-id="6a72c-214">效能檢查</span><span class="sxs-lookup"><span data-stu-id="6a72c-214">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="6a72c-215">判斷記憶體回收的時間長度。</span><span class="sxs-lookup"><span data-stu-id="6a72c-215">Determine the length of time in a garbage collection.</span></span>](#TimeInGC)<br /><br /> [<span data-ttu-id="6a72c-216">判斷造成記憶體回收的原因。</span><span class="sxs-lookup"><span data-stu-id="6a72c-216">Determine what caused a garbage collection.</span></span>](#Triggered)|

<a name="Issue_Gen0"></a>

### <a name="issue-generation-0-is-too-big"></a><span data-ttu-id="6a72c-217">問題：層代 0 太大</span><span class="sxs-lookup"><span data-stu-id="6a72c-217">Issue: Generation 0 Is Too Big</span></span>

<span data-ttu-id="6a72c-218">層代 0 可能在 64 位元系統上，有較大量的物件，特別是當您使用伺服器記憶體回收，而不是工作站記憶體回收時。</span><span class="sxs-lookup"><span data-stu-id="6a72c-218">Generation 0 is likely to have a larger number of objects on a 64-bit system, especially when you use server garbage collection instead of workstation garbage collection.</span></span> <span data-ttu-id="6a72c-219">這是因為在這些環境中觸發層代 0 記憶體回收的臨界值較高，層代 0 回收可能會變大許多。</span><span class="sxs-lookup"><span data-stu-id="6a72c-219">This is because the threshold to trigger a generation 0 garbage collection is higher in these environments, and generation 0 collections can get much bigger.</span></span> <span data-ttu-id="6a72c-220">當在觸發記憶體回收之前應用程式配置更多記憶體時，可提升效能。</span><span class="sxs-lookup"><span data-stu-id="6a72c-220">Performance is improved when an application allocates more memory before a garbage collection is triggered.</span></span>

<a name="Issue_HighCPU"></a>

### <a name="issue-cpu-usage-during-a-garbage-collection-is-too-high"></a><span data-ttu-id="6a72c-221">問題：在記憶體回收期間的 CPU 使用量太高</span><span class="sxs-lookup"><span data-stu-id="6a72c-221">Issue: CPU Usage During a Garbage Collection Is Too High</span></span>

<span data-ttu-id="6a72c-222">在記憶體回收期間的 CPU 使用量會很高。</span><span class="sxs-lookup"><span data-stu-id="6a72c-222">CPU usage will be high during a garbage collection.</span></span> <span data-ttu-id="6a72c-223">如果大量的處理序時間花在記憶體回收，則表示回收次數過於頻繁或是回收的持續時間太長。</span><span class="sxs-lookup"><span data-stu-id="6a72c-223">If a significant amount of process time is spent in a garbage collection, the number of collections is too frequent or the collection is lasting too long.</span></span> <span data-ttu-id="6a72c-224">Managed 堆積上物件配置率增加，會導致更頻繁地進行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-224">An increased allocation rate of objects on the managed heap causes garbage collection to occur more frequently.</span></span> <span data-ttu-id="6a72c-225">減少配置率可降低記憶體回收的頻率。</span><span class="sxs-lookup"><span data-stu-id="6a72c-225">Decreasing the allocation rate reduces the frequency of garbage collections.</span></span>

<span data-ttu-id="6a72c-226">您可以使用 `Allocated Bytes/second` 效能計數器，以監視配置率。</span><span class="sxs-lookup"><span data-stu-id="6a72c-226">You can monitor allocation rates by using the `Allocated Bytes/second` performance counter.</span></span> <span data-ttu-id="6a72c-227">如需詳細資訊，請參閱 [.net 中的效能計數器](../../framework/debug-trace-profile/performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-227">For more information, see [Performance Counters in .NET](../../framework/debug-trace-profile/performance-counters.md).</span></span>

<span data-ttu-id="6a72c-228">回收的持續時間主要是配置後存留之物件數目的因素。</span><span class="sxs-lookup"><span data-stu-id="6a72c-228">The duration of a collection is primarily a factor of the number of objects that survive after allocation.</span></span> <span data-ttu-id="6a72c-229">如果要收集許多物件，記憶體回收行程必須通過大量的記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-229">The garbage collector must go through a large amount of memory if many objects remain to be collected.</span></span> <span data-ttu-id="6a72c-230">壓縮存留者的工作相當耗時。</span><span class="sxs-lookup"><span data-stu-id="6a72c-230">The work to compact the survivors is time-consuming.</span></span> <span data-ttu-id="6a72c-231">若要判斷在回收期間處理的物件數目，請在指定層代的記憶體回收結尾處，在偵錯工具設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="6a72c-231">To determine how many objects were handled during a collection, set a breakpoint in the debugger at the end of a garbage collection for a specified generation.</span></span>

|<span data-ttu-id="6a72c-232">效能檢查</span><span class="sxs-lookup"><span data-stu-id="6a72c-232">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="6a72c-233">判斷高 CPU 使用量是否由於記憶體回收所造成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-233">Determine if high CPU usage is caused by garbage collection.</span></span>](#HighCPU)<br /><br /> [<span data-ttu-id="6a72c-234">在記憶體回收結尾處設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="6a72c-234">Set a breakpoint at the end of garbage collection.</span></span>](#GenBreak)|

## <a name="troubleshooting-guidelines"></a><span data-ttu-id="6a72c-235">疑難排解方針</span><span class="sxs-lookup"><span data-stu-id="6a72c-235">Troubleshooting Guidelines</span></span>

<span data-ttu-id="6a72c-236">本節描述當您開始調查時，應該考慮的方針。</span><span class="sxs-lookup"><span data-stu-id="6a72c-236">This section describes guidelines that you should consider as you begin your investigations.</span></span>

### <a name="workstation-or-server-garbage-collection"></a><span data-ttu-id="6a72c-237">工作站和伺服器記憶體回收</span><span class="sxs-lookup"><span data-stu-id="6a72c-237">Workstation or Server Garbage Collection</span></span>

<span data-ttu-id="6a72c-238">判斷您是否使用正確的記憶體回收類型。</span><span class="sxs-lookup"><span data-stu-id="6a72c-238">Determine if you are using the correct type of garbage collection.</span></span> <span data-ttu-id="6a72c-239">如果您的應用程式使用多個執行緒和物件執行個體，請使用伺服器記憶體回收，而不要使用工作站記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-239">If your application uses multiple threads and object instances, use server garbage collection instead of workstation garbage collection.</span></span> <span data-ttu-id="6a72c-240">伺服器記憶體回收會在多個執行緒上運作，而工作站記憶體回收則需要應用程式的多個執行個體執行自己的記憶體回收執行緒，且會競爭 CPU 時間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-240">Server garbage collection operates on multiple threads, whereas workstation garbage collection requires multiple instances of an application to run their own garbage collection threads and compete for CPU time.</span></span>

<span data-ttu-id="6a72c-241">具有低負載，且不常在背景中執行工作的應用程式，例如服務，可以使用工作站記憶體回收，並停用並行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-241">An application that has a low load and that performs tasks infrequently in the background, such as a service, could use workstation garbage collection with concurrent garbage collection disabled.</span></span>

### <a name="when-to-measure-the-managed-heap-size"></a><span data-ttu-id="6a72c-242">測量 Managed 堆積大小的時機</span><span class="sxs-lookup"><span data-stu-id="6a72c-242">When to Measure the Managed Heap Size</span></span>

<span data-ttu-id="6a72c-243">除非您使用程式碼剖析工具，否則您必須建立一致的測量模式，才能有效地診斷效能問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-243">Unless you are using a profiler, you will have to establish a consistent measuring pattern to effectively diagnose performance issues.</span></span> <span data-ttu-id="6a72c-244">建立排程時請考慮下列各點：</span><span class="sxs-lookup"><span data-stu-id="6a72c-244">Consider the following points to establish a schedule:</span></span>

- <span data-ttu-id="6a72c-245">如果您在層代 2 記憶體回收之後測量，整個 Managed 堆積都將沒有廢棄項目 (無作用物件)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-245">If you measure after a generation 2 garbage collection, the entire managed heap will be free of garbage (dead objects).</span></span>

- <span data-ttu-id="6a72c-246">如果層代 0 記憶體回收之後立即測量，此時尚不會回收層代 1 和 2 中的物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-246">If you measure immediately after a generation 0 garbage collection, the objects in generations 1 and 2 will not be collected yet.</span></span>

- <span data-ttu-id="6a72c-247">如果在記憶體回收之前立即測量，您會測量到記憶體回收開始之前最多的可能配置。</span><span class="sxs-lookup"><span data-stu-id="6a72c-247">If you measure immediately before a garbage collection, you will measure as much allocation as possible before the garbage collection starts.</span></span>

- <span data-ttu-id="6a72c-248">在記憶體回收期間測量會有問題，因為記憶體回收行程資料結構不在周遊的有效狀態，而且可能無法提供完整的結果。</span><span class="sxs-lookup"><span data-stu-id="6a72c-248">Measuring during a garbage collection is problematic, because the garbage collector data structures are not in a valid state for traversal and may not be able to give you the complete results.</span></span> <span data-ttu-id="6a72c-249">這是原廠設定。</span><span class="sxs-lookup"><span data-stu-id="6a72c-249">This is by design.</span></span>

- <span data-ttu-id="6a72c-250">當您使用工作站記憶體回收與並行記憶體回收時，回收的物件不會壓縮，因此堆積大小可能相同或更大 (分散可能讓它看起來似乎較大)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-250">When you are using workstation garbage collection with concurrent garbage collection, the reclaimed objects are not compacted, so the heap size can be the same or larger (fragmentation can make it appear to be larger).</span></span>

- <span data-ttu-id="6a72c-251">實體記憶體負載過高時，就會延遲層代 2 的並行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-251">Concurrent garbage collection on generation 2 is delayed when the physical memory load is too high.</span></span>

<span data-ttu-id="6a72c-252">下列程序描述如何設定中斷點，讓您可以測量 Managed 堆積。</span><span class="sxs-lookup"><span data-stu-id="6a72c-252">The following procedure describes how to set a breakpoint so that you can measure the managed heap.</span></span>

<a name="GenBreak"></a>

#### <a name="to-set-a-breakpoint-at-the-end-of-garbage-collection"></a><span data-ttu-id="6a72c-253">在記憶體回收結尾處設定中斷點</span><span class="sxs-lookup"><span data-stu-id="6a72c-253">To set a breakpoint at the end of garbage collection</span></span>

- <span data-ttu-id="6a72c-254">在載入 SOS 偵錯工具擴充功能的 WinDbg 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-254">In WinDbg with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="6a72c-255">**bp mscorwks!WKS::GCHeap::RestartEE "j (dwo(mscorwks!WKS::GCHeap::GcCondemnedGeneration)==2) 'kb';'g'"**</span><span class="sxs-lookup"><span data-stu-id="6a72c-255">**bp mscorwks!WKS::GCHeap::RestartEE "j (dwo(mscorwks!WKS::GCHeap::GcCondemnedGeneration)==2) 'kb';'g'"**</span></span>

  <span data-ttu-id="6a72c-256">其中 **GcCondemnedGeneration** 設為所需的層代。</span><span class="sxs-lookup"><span data-stu-id="6a72c-256">where **GcCondemnedGeneration** is set to the desired generation.</span></span> <span data-ttu-id="6a72c-257">此命令需要私用符號。</span><span class="sxs-lookup"><span data-stu-id="6a72c-257">This command requires private symbols.</span></span>

  <span data-ttu-id="6a72c-258">如果回收層代 2 物件，以進行記憶體回收之後，執行了 **RestartEE** ，則此命令會強制中斷。</span><span class="sxs-lookup"><span data-stu-id="6a72c-258">This command forces a break if **RestartEE** is executed after generation 2 objects have been reclaimed for garbage collection.</span></span>

  <span data-ttu-id="6a72c-259">在伺服器記憶體回收中，只有一個執行緒呼叫 **RestartEE** ，因此中斷點只會在層代 2 記憶體回收期間發生一次。</span><span class="sxs-lookup"><span data-stu-id="6a72c-259">In server garbage collection, only one thread calls **RestartEE** , so the breakpoint will occur only once during a generation 2 garbage collection.</span></span>

## <a name="performance-check-procedures"></a><span data-ttu-id="6a72c-260">效能檢查程序</span><span class="sxs-lookup"><span data-stu-id="6a72c-260">Performance Check Procedures</span></span>

<span data-ttu-id="6a72c-261">本節描述下列程序，以找出效能問題的原因：</span><span class="sxs-lookup"><span data-stu-id="6a72c-261">This section describes the following procedures to isolate the cause of your performance issue:</span></span>

- [<span data-ttu-id="6a72c-262">判斷問題是否由於記憶體回收所造成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-262">Determine whether the problem is caused by garbage collection.</span></span>](#IsGC)

- [<span data-ttu-id="6a72c-263">判斷記憶體不足例外狀況是否為 Managed。</span><span class="sxs-lookup"><span data-stu-id="6a72c-263">Determine whether the out-of-memory exception is managed.</span></span>](#OOMIsManaged)

- [<span data-ttu-id="6a72c-264">判斷可以保留多少虛擬記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-264">Determine how much virtual memory can be reserved.</span></span>](#GetVM)

- [<span data-ttu-id="6a72c-265">判斷是否有足夠的實體記憶體。</span><span class="sxs-lookup"><span data-stu-id="6a72c-265">Determine whether there is enough physical memory.</span></span>](#Physical)

- [<span data-ttu-id="6a72c-266">判斷 Managed 堆積正在認可的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-266">Determine how much memory the managed heap is committing.</span></span>](#ManagedHeapCommit)

- [<span data-ttu-id="6a72c-267">判斷 Managed 堆積保留的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-267">Determine how much memory the managed heap reserves.</span></span>](#ManagedHeapReserve)

- [<span data-ttu-id="6a72c-268">判斷層代 2 的大型物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-268">Determine large objects in generation 2.</span></span>](#ExamineGen2)

- [<span data-ttu-id="6a72c-269">判斷物件的參考。</span><span class="sxs-lookup"><span data-stu-id="6a72c-269">Determine references to objects.</span></span>](#ObjRef)

- [<span data-ttu-id="6a72c-270">判斷是否已執行完成項。</span><span class="sxs-lookup"><span data-stu-id="6a72c-270">Determine whether a finalizer has been run.</span></span>](#Induce)

- [<span data-ttu-id="6a72c-271">判斷是否有等候完成的物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-271">Determine whether there are objects waiting to be finalized.</span></span>](#Finalize)

- [<span data-ttu-id="6a72c-272">判斷 Managed 堆積中的可用空間數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-272">Determine the amount of free space in the managed heap.</span></span>](#Fragmented)

- [<span data-ttu-id="6a72c-273">判斷被固定的物件數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-273">Determine the number of pinned objects.</span></span>](#Pinned)

- [<span data-ttu-id="6a72c-274">判斷記憶體回收的時間長度。</span><span class="sxs-lookup"><span data-stu-id="6a72c-274">Determine the length of time in a garbage collection.</span></span>](#TimeInGC)

- [<span data-ttu-id="6a72c-275">判斷觸發記憶體回收的原因。</span><span class="sxs-lookup"><span data-stu-id="6a72c-275">Determine what triggered a garbage collection.</span></span>](#Triggered)

- [<span data-ttu-id="6a72c-276">判斷高 CPU 使用量是否由於記憶體回收所造成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-276">Determine whether high CPU usage is caused by garbage collection.</span></span>](#HighCPU)

<a name="IsGC"></a>

### <a name="to-determine-whether-the-problem-is-caused-by-garbage-collection"></a><span data-ttu-id="6a72c-277">判斷問題是否由於記憶體回收所造成</span><span class="sxs-lookup"><span data-stu-id="6a72c-277">To determine whether the problem is caused by garbage collection</span></span>

- <span data-ttu-id="6a72c-278">檢查下列兩個記憶體效能計數器：</span><span class="sxs-lookup"><span data-stu-id="6a72c-278">Examine the following two memory performance counters:</span></span>

  - <span data-ttu-id="6a72c-279">**% Time IN GC** 。</span><span class="sxs-lookup"><span data-stu-id="6a72c-279">**% Time in GC** .</span></span> <span data-ttu-id="6a72c-280">顯示自上次記憶體回收循環後所花費在執行記憶體回收的已耗用時間百分比。</span><span class="sxs-lookup"><span data-stu-id="6a72c-280">Displays the percentage of elapsed time that was spent performing a garbage collection after the last garbage collection cycle.</span></span> <span data-ttu-id="6a72c-281">使用此計數器來判斷是否記憶體回收行程花費太多時間才讓 Managed 堆積的空間可供使用。</span><span class="sxs-lookup"><span data-stu-id="6a72c-281">Use this counter to determine whether the garbage collector is spending too much time to make managed heap space available.</span></span> <span data-ttu-id="6a72c-282">如果花費在記憶體回收的時間很短，可能表示 Managed 堆積以外的資源問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-282">If the time spent in garbage collection is relatively low, that could indicate a resource problem outside the managed heap.</span></span> <span data-ttu-id="6a72c-283">與並行或背景記憶體回收相關時，這個計數器可能不正確。</span><span class="sxs-lookup"><span data-stu-id="6a72c-283">This counter may not be accurate when concurrent or background garbage collection is involved.</span></span>

  - <span data-ttu-id="6a72c-284">**認可的總位元組數** 。</span><span class="sxs-lookup"><span data-stu-id="6a72c-284">**# Total committed Bytes** .</span></span> <span data-ttu-id="6a72c-285">顯示記憶體回收行程目前已認可的虛擬記憶體數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-285">Displays the amount of virtual memory currently committed by the garbage collector.</span></span> <span data-ttu-id="6a72c-286">使用此計數器來判斷記憶體回收行程所耗用的記憶體是否佔應用程式所使用記憶體的過多數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-286">Use this counter to determine whether the memory consumed by the garbage collector is an excessive portion of the memory that your application uses.</span></span>

  <span data-ttu-id="6a72c-287">大部分的記憶體效能計數器會在每次記憶體回收結束時更新。</span><span class="sxs-lookup"><span data-stu-id="6a72c-287">Most of the memory performance counters are updated at the end of each garbage collection.</span></span> <span data-ttu-id="6a72c-288">因此，它們可能無法反映您要取得相關資訊的目前狀況。</span><span class="sxs-lookup"><span data-stu-id="6a72c-288">Therefore, they may not reflect the current conditions that you want information about.</span></span>

<a name="OOMIsManaged"></a>

### <a name="to-determine-whether-the-out-of-memory-exception-is-managed"></a><span data-ttu-id="6a72c-289">判斷記憶體不足例外狀況是否為 Managed</span><span class="sxs-lookup"><span data-stu-id="6a72c-289">To determine whether the out-of-memory exception is managed</span></span>

1. <span data-ttu-id="6a72c-290">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入列印例外狀況 ( **pe** ) 命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-290">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the print exception ( **pe** ) command:</span></span>

    <span data-ttu-id="6a72c-291">**！ pe**</span><span class="sxs-lookup"><span data-stu-id="6a72c-291">**!pe**</span></span>

    <span data-ttu-id="6a72c-292">如果例外狀況為 Managed，<xref:System.OutOfMemoryException> 會顯示為例外狀況類型，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-292">If the exception is managed, <xref:System.OutOfMemoryException> is displayed as the exception type, as shown in the following example.</span></span>

    ```console
    Exception object: 39594518
    Exception type: System.OutOfMemoryException
    Message: <none>
    InnerException: <none>
    StackTrace (generated):
    ```

2. <span data-ttu-id="6a72c-293">如果輸出未指定例外狀況，您必須判斷記憶體不足例外狀況是來自哪一個執行緒。</span><span class="sxs-lookup"><span data-stu-id="6a72c-293">If the output does not specify an exception, you have to determine which thread the out-of-memory exception is from.</span></span> <span data-ttu-id="6a72c-294">在偵錯工具中輸入下列命令，顯示所有執行緒與其呼叫堆疊：</span><span class="sxs-lookup"><span data-stu-id="6a72c-294">Type the following command in the debugger to show all the threads with their call stacks:</span></span>

    <span data-ttu-id="6a72c-295">**~\*K b**</span><span class="sxs-lookup"><span data-stu-id="6a72c-295">**~\*kb**</span></span>

    <span data-ttu-id="6a72c-296">堆疊具有例外狀況呼叫的執行緒會以 `RaiseTheException` 引數表示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-296">The thread with the stack that has exception calls is indicated by the `RaiseTheException` argument.</span></span> <span data-ttu-id="6a72c-297">這是 Managed 例外狀況物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-297">This is the managed exception object.</span></span>

    ```console
    28adfb44 7923918f 5b61f2b4 00000000 5b61f2b4 mscorwks!RaiseTheException+0xa0
    ```

3. <span data-ttu-id="6a72c-298">您可以使用下列命令來傾印巢狀例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6a72c-298">You can use the following command to dump nested exceptions.</span></span>

    <span data-ttu-id="6a72c-299">**!pe -nested**</span><span class="sxs-lookup"><span data-stu-id="6a72c-299">**!pe -nested**</span></span>

    <span data-ttu-id="6a72c-300">如果找不到任何例外狀況，表示記憶體不足例外狀況是源自於 Unmanaged 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6a72c-300">If you do not find any exceptions, the out-of-memory exception originated from unmanaged code.</span></span>

<a name="GetVM"></a>

### <a name="to-determine-how-much-virtual-memory-can-be-reserved"></a><span data-ttu-id="6a72c-301">判斷可以保留多少虛擬記憶體</span><span class="sxs-lookup"><span data-stu-id="6a72c-301">To determine how much virtual memory can be reserved</span></span>

- <span data-ttu-id="6a72c-302">在載入 SOS 偵錯工具擴充功能的 WinDbg 中，輸入下列命令，取得最大的可用區域：</span><span class="sxs-lookup"><span data-stu-id="6a72c-302">In WinDbg with the SOS debugger extension loaded, type the following command to get the largest free region:</span></span>

  <span data-ttu-id="6a72c-303">**!address -summary**</span><span class="sxs-lookup"><span data-stu-id="6a72c-303">**!address -summary**</span></span>

  <span data-ttu-id="6a72c-304">最大可用區域會顯示在下列輸出中。</span><span class="sxs-lookup"><span data-stu-id="6a72c-304">The largest free region is displayed as shown in the following output.</span></span>

  ```console
  Largest free region: Base 54000000 - Size 0003A980
  ```

  <span data-ttu-id="6a72c-305">在此範例中，最大可用區域的大小大約為 24000 KB (十六進位為 3A980)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-305">In this example, the size of the largest free region is approximately 24000 KB (3A980 in hexadecimal).</span></span> <span data-ttu-id="6a72c-306">此區域是遠小於記憶體回收行程針對區段所需。</span><span class="sxs-lookup"><span data-stu-id="6a72c-306">This region is much smaller than what the garbage collector needs for a segment.</span></span>

  <span data-ttu-id="6a72c-307">-或-</span><span class="sxs-lookup"><span data-stu-id="6a72c-307">-or-</span></span>

- <span data-ttu-id="6a72c-308">使用 **vmstat** 命令︰</span><span class="sxs-lookup"><span data-stu-id="6a72c-308">Use the **vmstat** command:</span></span>

  <span data-ttu-id="6a72c-309">**!vmstat**</span><span class="sxs-lookup"><span data-stu-id="6a72c-309">**!vmstat**</span></span>

  <span data-ttu-id="6a72c-310">最大可用區域是 MAXIMUM 資料行中的最大值，如下列輸出所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-310">The largest free region is the largest value in the MAXIMUM column, as shown in the following output.</span></span>

  ```console
  TYPE        MINIMUM   MAXIMUM     AVERAGE   BLK COUNT   TOTAL
  ~~~~        ~~~~~~~   ~~~~~~~     ~~~~~~~   ~~~~~~~~~~  ~~~~
  Free:
  Small       8K        64K         46K       36          1,671K
  Medium      80K       864K        349K      3           1,047K
  Large       1,384K    1,278,848K  151,834K  12          1,822,015K
  Summary     8K        1,278,848K  35,779K   51          1,824,735K
  ```

<a name="Physical"></a>

### <a name="to-determine-whether-there-is-enough-physical-memory"></a><span data-ttu-id="6a72c-311">判斷是否有足夠的實體記憶體</span><span class="sxs-lookup"><span data-stu-id="6a72c-311">To determine whether there is enough physical memory</span></span>

1. <span data-ttu-id="6a72c-312">啟動 Windows 工作管理員。</span><span class="sxs-lookup"><span data-stu-id="6a72c-312">Start Windows Task Manager.</span></span>

2. <span data-ttu-id="6a72c-313">在 [效能]  索引標籤上，查看已認可的值。</span><span class="sxs-lookup"><span data-stu-id="6a72c-313">On the **Performance** tab, look at the committed value.</span></span> <span data-ttu-id="6a72c-314">(在 Windows 7 中，查看 [系統群組]  中的 [認可 (KB)]  。)</span><span class="sxs-lookup"><span data-stu-id="6a72c-314">(In Windows 7, look at **Commit (KB)** in the **System group** .)</span></span>

    <span data-ttu-id="6a72c-315">如果 [總計]  很接近 [限制]  ，則您的實體記憶體不足。</span><span class="sxs-lookup"><span data-stu-id="6a72c-315">If the **Total** is close to the **Limit** , you are running low on physical memory.</span></span>

<a name="ManagedHeapCommit"></a>

### <a name="to-determine-how-much-memory-the-managed-heap-is-committing"></a><span data-ttu-id="6a72c-316">判斷 Managed 堆積正在認可的記憶體數量</span><span class="sxs-lookup"><span data-stu-id="6a72c-316">To determine how much memory the managed heap is committing</span></span>

- <span data-ttu-id="6a72c-317">使用 `# Total committed bytes` 記憶體效能計數器，以取得 Managed 堆積正在認可的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-317">Use the `# Total committed bytes` memory performance counter to get the number of bytes that the managed heap is committing.</span></span> <span data-ttu-id="6a72c-318">記憶體回收行程會視需要認可區段上的區塊 (chunk)，而不是同時全部認可。</span><span class="sxs-lookup"><span data-stu-id="6a72c-318">The garbage collector commits chunks on a segment as needed, not all at the same time.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6a72c-319">請勿使用 `# Bytes in all Heaps` 效能計數器，因為它不代表 Managed 堆積的實際記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-319">Do not use the `# Bytes in all Heaps` performance counter, because it does not represent actual memory usage by the managed heap.</span></span> <span data-ttu-id="6a72c-320">層代的大小包含在此值中，且為其實際閾值大小，也就是層代裝滿物件時引發記憶體回收的大小。</span><span class="sxs-lookup"><span data-stu-id="6a72c-320">The size of a generation is included in this value and is actually its threshold size, that is, the size that induces a garbage collection if the generation is filled with objects.</span></span> <span data-ttu-id="6a72c-321">因此，這個值通常是零。</span><span class="sxs-lookup"><span data-stu-id="6a72c-321">Therefore, this value is usually zero.</span></span>

<a name="ManagedHeapReserve"></a>

### <a name="to-determine-how-much-memory-the-managed-heap-reserves"></a><span data-ttu-id="6a72c-322">判斷 Managed 堆積保留的記憶體數量</span><span class="sxs-lookup"><span data-stu-id="6a72c-322">To determine how much memory the managed heap reserves</span></span>

- <span data-ttu-id="6a72c-323">使用 `# Total reserved bytes` 記憶體效能計數器。</span><span class="sxs-lookup"><span data-stu-id="6a72c-323">Use the `# Total reserved bytes` memory performance counter.</span></span>

  <span data-ttu-id="6a72c-324">記憶體回收行程會以區段來保留記憶體，您可以使用 **eeheap** 命令來判斷區段開始的位置。</span><span class="sxs-lookup"><span data-stu-id="6a72c-324">The garbage collector reserves memory in segments, and you can determine where a segment starts by using the **eeheap** command.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6a72c-325">雖然您可以判斷記憶體回收行程配置給每個區段的記憶體數量，但區段大小會依實作而定，而且隨時可能變更，包括定期更新。</span><span class="sxs-lookup"><span data-stu-id="6a72c-325">Although you can determine the amount of memory the garbage collector allocates for each segment, segment size is implementation-specific and is subject to change at any time, including in periodic updates.</span></span> <span data-ttu-id="6a72c-326">您的應用程式永遠都不應該對相關或根據特定區段的大小做出假設，也不應嘗試設定區段配置的可用記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-326">Your app should never make assumptions about or depend on a particular segment size, nor should it attempt to configure the amount of memory available for segment allocations.</span></span>

- <span data-ttu-id="6a72c-327">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-327">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="6a72c-328">**!eeheap -gc**</span><span class="sxs-lookup"><span data-stu-id="6a72c-328">**!eeheap -gc**</span></span>

  <span data-ttu-id="6a72c-329">結果如下所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-329">The result is as follows.</span></span>

  ```console
  Number of GC Heaps: 2
  ------------------------------
  Heap 0 (002db550)
  generation 0 starts at 0x02abe29c
  generation 1 starts at 0x02abdd08
  generation 2 starts at 0x02ab0038
  ephemeral segment allocation context: none
    segment    begin allocated     size
  02ab0000 02ab0038  02aceff4 0x0001efbc(126908)
  Large object heap starts at 0x0aab0038
    segment    begin allocated     size
  0aab0000 0aab0038  0aab2278 0x00002240(8768)
  Heap Size   0x211fc(135676)
  ------------------------------
  Heap 1 (002dc958)
  generation 0 starts at 0x06ab1bd8
  generation 1 starts at 0x06ab1bcc
  generation 2 starts at 0x06ab0038
  ephemeral segment allocation context: none
    segment    begin allocated     size
  06ab0000 06ab0038  06ab3be4 0x00003bac(15276)
  Large object heap starts at 0x0cab0038
    segment    begin allocated     size
  0cab0000 0cab0038  0cab0048 0x00000010(16)
  Heap Size    0x3bbc(15292)
  ------------------------------
  GC Heap Size   0x24db8(150968)
  ```

  <span data-ttu-id="6a72c-330">「區段」所指定的位址是區段的起始位址。</span><span class="sxs-lookup"><span data-stu-id="6a72c-330">The addresses indicated by "segment" are the starting addresses of the segments.</span></span>

<a name="ExamineGen2"></a>

### <a name="to-determine-large-objects-in-generation-2"></a><span data-ttu-id="6a72c-331">判斷層代 2 的大型物件</span><span class="sxs-lookup"><span data-stu-id="6a72c-331">To determine large objects in generation 2</span></span>

- <span data-ttu-id="6a72c-332">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-332">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="6a72c-333">**!dumpheap –stat**</span><span class="sxs-lookup"><span data-stu-id="6a72c-333">**!dumpheap –stat**</span></span>

  <span data-ttu-id="6a72c-334">如果 Managed 堆積很大， **dumpheap** 可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-334">If the managed heap is big, **dumpheap** may take a while to finish.</span></span>

  <span data-ttu-id="6a72c-335">您可以從輸出的最後幾行開始分析，因為它們列出使用最多空間的物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-335">You can start analyzing from the last few lines of the output, because they list the objects that use the most space.</span></span> <span data-ttu-id="6a72c-336">例如：</span><span class="sxs-lookup"><span data-stu-id="6a72c-336">For example:</span></span>

  ```console
  2c6108d4   173712     14591808 DevExpress.XtraGrid.Views.Grid.ViewInfo.GridCellInfo
  00155f80      533     15216804      Free
  7a747c78   791070     15821400 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700930     19626040 System.Collections.Specialized.ListDictionary
  2c64e36c    78644     20762016 DevExpress.XtraEditors.ViewInfo.TextEditViewInfo
  79124228   121143     29064120 System.Object[]
  035f0ee4    81626     35588936 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  791242ec    40182     90664128 System.Collections.Hashtable+bucket[]
  790fa3e0  3154024    137881448 System.String
  Total 8454945 objects
  ```

  <span data-ttu-id="6a72c-337">所列的最後一個物件是一個字串，而且會佔用最多的空間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-337">The last object listed is a string and occupies the most space.</span></span> <span data-ttu-id="6a72c-338">您可以檢查應用程式，了解如何最佳化您的字串物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-338">You can examine your application to see how your string objects can be optimized.</span></span> <span data-ttu-id="6a72c-339">若要查看介於 150 到 200 個位元組的字串，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-339">To see strings that are between 150 and 200 bytes, type the following:</span></span>

  <span data-ttu-id="6a72c-340">**!dumpheap -type System.String -min 150 -max 200**</span><span class="sxs-lookup"><span data-stu-id="6a72c-340">**!dumpheap -type System.String -min 150 -max 200**</span></span>

  <span data-ttu-id="6a72c-341">結果的範例如下。</span><span class="sxs-lookup"><span data-stu-id="6a72c-341">An example of the results is as follows.</span></span>

  ```console
  Address  MT           Size  Gen
  1875d2c0 790fa3e0      152    2 System.String HighlightNullStyle_Blotter_PendingOrder-11_Blotter_PendingOrder-11
  …
  ```

  <span data-ttu-id="6a72c-342">針對識別碼使用整數而不使用字串，可能會更有效率。</span><span class="sxs-lookup"><span data-stu-id="6a72c-342">Using an integer instead of a string for an ID can be more efficient.</span></span> <span data-ttu-id="6a72c-343">如果相同的字串重複數千次，請考慮字串拘留 (string interning)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-343">If the same string is being repeated thousands of times, consider string interning.</span></span> <span data-ttu-id="6a72c-344">如需有關字串拘留的詳細資訊，請參閱 <xref:System.String.Intern%2A?displayProperty=nameWithType> 方法的參考主題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-344">For more information about string interning, see the reference topic for the <xref:System.String.Intern%2A?displayProperty=nameWithType> method.</span></span>

<a name="ObjRef"></a>

### <a name="to-determine-references-to-objects"></a><span data-ttu-id="6a72c-345">判斷物件的參考</span><span class="sxs-lookup"><span data-stu-id="6a72c-345">To determine references to objects</span></span>

- <span data-ttu-id="6a72c-346">在載入 SOS 偵錯工具擴充功能的 WinDbg 中，輸入下列命令，列出物件的參考：</span><span class="sxs-lookup"><span data-stu-id="6a72c-346">In WinDbg with the SOS debugger extension loaded, type the following command to list references to objects:</span></span>

  <span data-ttu-id="6a72c-347">**!gcroot**</span><span class="sxs-lookup"><span data-stu-id="6a72c-347">**!gcroot**</span></span>

  `-or-`

- <span data-ttu-id="6a72c-348">若要判斷特定物件的參考，請包含位址：</span><span class="sxs-lookup"><span data-stu-id="6a72c-348">To determine the references for a specific object, include the address:</span></span>

  <span data-ttu-id="6a72c-349">**!gcroot 1c37b2ac**</span><span class="sxs-lookup"><span data-stu-id="6a72c-349">**!gcroot 1c37b2ac**</span></span>

  <span data-ttu-id="6a72c-350">在堆疊上找到的根可能是誤判。</span><span class="sxs-lookup"><span data-stu-id="6a72c-350">Roots found on stacks may be false positives.</span></span> <span data-ttu-id="6a72c-351">如需詳細資訊，請參閱 `!help gcroot` 命令。</span><span class="sxs-lookup"><span data-stu-id="6a72c-351">For more information, use the command `!help gcroot`.</span></span>

  ```console
  ebx:Root:19011c5c(System.Windows.Forms.Application+ThreadContext)->
  19010b78(DemoApp.FormDemoApp)->
  19011158(System.Windows.Forms.PropertyStore)->
  … [omitted]
  1c3745ec(System.Data.DataTable)->
  1c3747a8(System.Data.DataColumnCollection)->
  1c3747f8(System.Collections.Hashtable)->
  1c376590(System.Collections.Hashtable+bucket[])->
  1c376c98(System.Data.DataColumn)->
  1c37b270(System.Data.Common.DoubleStorage)->
  1c37b2ac(System.Double[])
  Scan Thread 0 OSTHread 99c
  Scan Thread 6 OSTHread 484
  ```

  <span data-ttu-id="6a72c-352">**gcroot** 命令可能會執行很長的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-352">The **gcroot** command can take a long time to finish.</span></span> <span data-ttu-id="6a72c-353">不由記憶體回收所回收的任何物件便是實際物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-353">Any object that is not reclaimed by garbage collection is a live object.</span></span> <span data-ttu-id="6a72c-354">這表示某些根是直接或間接緊守住物件，所以 **gcroot** 應該傳回物件的路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="6a72c-354">This means that some root is directly or indirectly holding onto the object, so **gcroot** should return path information to the object.</span></span> <span data-ttu-id="6a72c-355">您應該檢查傳回的圖形，並查看為什麼仍然參考這些物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-355">You should examine the graphs returned and see why these objects are still referenced.</span></span>

<a name="Induce"></a>

### <a name="to-determine-whether-a-finalizer-has-been-run"></a><span data-ttu-id="6a72c-356">判斷是否已執行完成項</span><span class="sxs-lookup"><span data-stu-id="6a72c-356">To determine whether a finalizer has been run</span></span>

- <span data-ttu-id="6a72c-357">執行測試程式，其中包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6a72c-357">Run a test program that contains the following code:</span></span>

  ```csharp
  GC.Collect();
  GC.WaitForPendingFinalizers();
  GC.Collect();
  ```

  <span data-ttu-id="6a72c-358">如果測試可以解決此問題，這表示記憶體回收行程未回收物件，因為這些物件的完成項已暫止。</span><span class="sxs-lookup"><span data-stu-id="6a72c-358">If the test resolves the problem, this means that the garbage collector was not reclaiming objects, because the finalizers for those objects had been suspended.</span></span> <span data-ttu-id="6a72c-359"><xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> 方法讓完成項能完成其工作，並修正問題。</span><span class="sxs-lookup"><span data-stu-id="6a72c-359">The <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> method enables the finalizers to complete their tasks, and fixes the problem.</span></span>

<a name="Finalize"></a>

### <a name="to-determine-whether-there-are-objects-waiting-to-be-finalized"></a><span data-ttu-id="6a72c-360">判斷是否有等候完成的物件</span><span class="sxs-lookup"><span data-stu-id="6a72c-360">To determine whether there are objects waiting to be finalized</span></span>

1. <span data-ttu-id="6a72c-361">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-361">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

    <span data-ttu-id="6a72c-362">**!finalizequeue**</span><span class="sxs-lookup"><span data-stu-id="6a72c-362">**!finalizequeue**</span></span>

    <span data-ttu-id="6a72c-363">查看準備好進行最終處理的物件數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-363">Look at the number of objects that are ready for finalization.</span></span> <span data-ttu-id="6a72c-364">如果數量很高，您必須檢查為什麼這些完成項完全沒有進度，或進行的速度不夠快。</span><span class="sxs-lookup"><span data-stu-id="6a72c-364">If the number is high, you must examine why these finalizers cannot progress at all or cannot progress fast enough.</span></span>

2. <span data-ttu-id="6a72c-365">若要取得執行緒的輸出，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-365">To get an output of threads, type the following command:</span></span>

    <span data-ttu-id="6a72c-366">**threads -special**</span><span class="sxs-lookup"><span data-stu-id="6a72c-366">**threads -special**</span></span>

    <span data-ttu-id="6a72c-367">這個命令會提供如下所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="6a72c-367">This command provides output such as the following.</span></span>

    ```console
       OSID     Special thread type
    2    cd0    DbgHelper
    3    c18    Finalizer
    4    df0    GC SuspendEE
    ```

    <span data-ttu-id="6a72c-368">完成項執行緒會指出目前正在執行哪一個完成項 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-368">The finalizer thread indicates which finalizer, if any, is currently being run.</span></span> <span data-ttu-id="6a72c-369">當完成項執行緒未在執行任何完成項時，它正在等候事件來告訴它要執行其工作。</span><span class="sxs-lookup"><span data-stu-id="6a72c-369">When a finalizer thread is not running any finalizers, it is waiting for an event to tell it to do its work.</span></span> <span data-ttu-id="6a72c-370">大多數情況下會看見完成項執行緒處於此狀態，是因為它以 THREAD_HIGHEST_PRIORITY 執行，並且應該非常快速地完成執行完成項 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-370">Most of the time you will see the finalizer thread in this state because it runs at THREAD_HIGHEST_PRIORITY and is supposed to finish running finalizers, if any, very quickly.</span></span>

<a name="Fragmented"></a>

### <a name="to-determine-the-amount-of-free-space-in-the-managed-heap"></a><span data-ttu-id="6a72c-371">判斷 Managed 堆積中的可用空間數量</span><span class="sxs-lookup"><span data-stu-id="6a72c-371">To determine the amount of free space in the managed heap</span></span>

- <span data-ttu-id="6a72c-372">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-372">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="6a72c-373">**!dumpheap -type Free -stat**</span><span class="sxs-lookup"><span data-stu-id="6a72c-373">**!dumpheap -type Free -stat**</span></span>

  <span data-ttu-id="6a72c-374">此命令會顯示 Managed 堆積中所有可用物件的大小總計，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-374">This command displays the total size of all the free objects on the managed heap, as shown in the following example.</span></span>

  ```console
  total 230 objects
  Statistics:
        MT    Count    TotalSize Class Name
  00152b18      230     40958584      Free
  Total 230 objects
  ```

- <span data-ttu-id="6a72c-375">若要判斷層代 0 中的可用空間，請輸入下列命令以取得依層代的記憶體耗用量資訊：</span><span class="sxs-lookup"><span data-stu-id="6a72c-375">To determine the free space in generation 0, type the following command for memory consumption information by generation:</span></span>

  <span data-ttu-id="6a72c-376">**!eeheap -gc**</span><span class="sxs-lookup"><span data-stu-id="6a72c-376">**!eeheap -gc**</span></span>

  <span data-ttu-id="6a72c-377">這個命令會顯示與下列類似的輸出。</span><span class="sxs-lookup"><span data-stu-id="6a72c-377">This command displays output similar to the following.</span></span> <span data-ttu-id="6a72c-378">最後一行顯示暫時區段。</span><span class="sxs-lookup"><span data-stu-id="6a72c-378">The last line shows the ephemeral segment.</span></span>

  ```console
  Heap 0 (0015ad08)
  generation 0 starts at 0x49521f8c
  generation 1 starts at 0x494d7f64
  generation 2 starts at 0x007f0038
  ephemeral segment allocation context: none
  segment  begin     allocated  size
  00178250 7a80d84c  7a82f1cc   0x00021980(137600)
  00161918 78c50e40  78c7056c   0x0001f72c(128812)
  007f0000 007f0038  047eed28   0x03ffecf0(67103984)
  3a120000 3a120038  3a3e84f8   0x002c84c0(2917568)
  46120000 46120038  49e05d04   0x03ce5ccc(63855820)
  ```

- <span data-ttu-id="6a72c-379">計算層代 0 所使用的空間：</span><span class="sxs-lookup"><span data-stu-id="6a72c-379">Calculate the space used by generation 0:</span></span>

  <span data-ttu-id="6a72c-380">**?49e05d04-0x49521f8c**</span><span class="sxs-lookup"><span data-stu-id="6a72c-380">**? 49e05d04-0x49521f8c**</span></span>

  <span data-ttu-id="6a72c-381">結果如下所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-381">The result is as follows.</span></span> <span data-ttu-id="6a72c-382">層代 0 大約 9 MB。</span><span class="sxs-lookup"><span data-stu-id="6a72c-382">Generation 0 is approximately 9 MB.</span></span>

  ```console
  Evaluate expression: 9321848 = 008e3d78
  ```

- <span data-ttu-id="6a72c-383">下列命令會傾印在層代 0 範圍內的可用空間：</span><span class="sxs-lookup"><span data-stu-id="6a72c-383">The following command dumps the free space within the generation 0 range:</span></span>

  <span data-ttu-id="6a72c-384">**!dumpheap -type Free -stat 0x49521f8c 49e05d04**</span><span class="sxs-lookup"><span data-stu-id="6a72c-384">**!dumpheap -type Free -stat 0x49521f8c 49e05d04**</span></span>

  <span data-ttu-id="6a72c-385">結果如下所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-385">The result is as follows.</span></span>

  ```console
  ------------------------------
  Heap 0
  total 409 objects
  ------------------------------
  Heap 1
  total 0 objects
  ------------------------------
  Heap 2
  total 0 objects
  ------------------------------
  Heap 3
  total 0 objects
  ------------------------------
  total 409 objects
  Statistics:
        MT    Count TotalSize Class Name
  0015a498      409   7296540      Free
  Total 409 objects
  ```

  <span data-ttu-id="6a72c-386">此輸出顯示堆積的層代 0 部分使用 9 MB 的物件空間，並有 7 MB 可用。</span><span class="sxs-lookup"><span data-stu-id="6a72c-386">This output shows that the generation 0 portion of the heap is using 9 MB of space for objects and has 7 MB free.</span></span> <span data-ttu-id="6a72c-387">這項分析顯示層代 0 對分散的影響程度。</span><span class="sxs-lookup"><span data-stu-id="6a72c-387">This analysis shows the extent to which generation 0 contributes to fragmentation.</span></span> <span data-ttu-id="6a72c-388">在計算長期物件的分散原因時，此堆積使用量應該從總數量扣除。</span><span class="sxs-lookup"><span data-stu-id="6a72c-388">This amount of heap usage should be discounted from the total amount as the cause of fragmentation by long-term objects.</span></span>

<a name="Pinned"></a>

### <a name="to-determine-the-number-of-pinned-objects"></a><span data-ttu-id="6a72c-389">判斷被固定的物件數目</span><span class="sxs-lookup"><span data-stu-id="6a72c-389">To determine the number of pinned objects</span></span>

- <span data-ttu-id="6a72c-390">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-390">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="6a72c-391">**!gchandles**</span><span class="sxs-lookup"><span data-stu-id="6a72c-391">**!gchandles**</span></span>

  <span data-ttu-id="6a72c-392">顯示的統計資料包括固定控制代碼數目，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6a72c-392">The statistics displayed includes the number of pinned handles, as the following example shows.</span></span>

  ```console
  GC Handle Statistics:
  Strong Handles:      29
  Pinned Handles:      10
  ```

<a name="TimeInGC"></a>

### <a name="to-determine-the-length-of-time-in-a-garbage-collection"></a><span data-ttu-id="6a72c-393">判斷記憶體回收的時間長度</span><span class="sxs-lookup"><span data-stu-id="6a72c-393">To determine the length of time in a garbage collection</span></span>

- <span data-ttu-id="6a72c-394">檢查 `% Time in GC` 記憶體效能計數器。</span><span class="sxs-lookup"><span data-stu-id="6a72c-394">Examine the `% Time in GC` memory performance counter.</span></span>

  <span data-ttu-id="6a72c-395">值的計算是使用取樣間隔時間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-395">The value is calculated by using a sample interval time.</span></span> <span data-ttu-id="6a72c-396">由於計數器會在每次記憶體回收結束時更新，如果在間隔期間未發生任何回收，則目前的取樣值將會與前一個取樣值相同。</span><span class="sxs-lookup"><span data-stu-id="6a72c-396">Because the counters are updated at the end of each garbage collection, the current sample will have the same value as the previous sample if no collections occurred during the interval.</span></span>

  <span data-ttu-id="6a72c-397">回收時間是將取樣間隔時間乘上百分比值而取得。</span><span class="sxs-lookup"><span data-stu-id="6a72c-397">Collection time is obtained by multiplying the sample interval time with the percentage value.</span></span>

  <span data-ttu-id="6a72c-398">下列資料顯示四個兩秒的取樣間隔，也就是 8 秒的研究。</span><span class="sxs-lookup"><span data-stu-id="6a72c-398">The following data shows four sampling intervals of two seconds, for an 8-second study.</span></span> <span data-ttu-id="6a72c-399">`Gen0`、`Gen1` 和 `Gen2` 資料行會顯示在該層代的間隔期間發生的記憶體回收數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-399">The `Gen0`, `Gen1`, and `Gen2` columns show the number of garbage collections that occurred during that interval for that generation.</span></span>

  ```console
  Interval    Gen0    Gen1    Gen2    % Time in GC
          1       9       3       1              10
          2      10       3       1               1
          3      11       3       1               3
          4      11       3       1               3
  ```

  <span data-ttu-id="6a72c-400">這項資訊不會顯示記憶體回收發生的時間，但您可以判斷在時間間隔中發生的記憶體回收數目。</span><span class="sxs-lookup"><span data-stu-id="6a72c-400">This information does not show when the garbage collection occurred, but you can determine the number of garbage collections that occurred in an interval of time.</span></span> <span data-ttu-id="6a72c-401">假設在最壞的情況下，第十次層代 0 記憶體回收在第二個間隔開始時完成，而第十一次層代 0 記憶體回收在第五個間隔結束時完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-401">Assuming the worst case, the tenth generation 0 garbage collection finished at the start of the second interval, and the eleventh generation 0 garbage collection finished at the end of the fifth interval.</span></span> <span data-ttu-id="6a72c-402">第十次記憶體回收與第十一次記憶體回收結束之間的時間約 2 秒，而且效能計數器顯示 3%，因此第十一次層代 0 記憶體回收的持續時間為 (2 秒 \* 3% = 60 毫秒)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-402">The time between the end of the tenth and the end of the eleventh garbage collection is about 2 seconds, and the performance counter shows 3%, so the duration of the eleventh generation 0 garbage collection was (2 seconds \* 3% = 60ms).</span></span>

  <span data-ttu-id="6a72c-403">在此範例中，有 5 個週期。</span><span class="sxs-lookup"><span data-stu-id="6a72c-403">In this example, there are 5 periods.</span></span>

  ```console
  Interval    Gen0    Gen1    Gen2     % Time in GC
          1       9       3       1                3
          2      10       3       1                1
          3      11       4       2                1
          4      11       4       2                1
          5      11       4       2               20
  ```

  <span data-ttu-id="6a72c-404">第二次層代 2 記憶體回收在第三個間隔期間開始，並在第五個間隔完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-404">The second generation 2 garbage collection started during the third interval and finished at the fifth interval.</span></span> <span data-ttu-id="6a72c-405">假設在最壞的情況下，最後一次記憶體回收是針對層代 0 回收，其在第二個間隔開始時完成，且層代 2 記憶體回收在第五個間隔結束時完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-405">Assuming the worst case, the last garbage collection was for a generation 0 collection that finished at the start of the second interval, and the generation 2 garbage collection finished at the end of the fifth interval.</span></span> <span data-ttu-id="6a72c-406">因此，層代 0 記憶體回收結束與層代 2 記憶體回收結束之間的時間是 4 秒。</span><span class="sxs-lookup"><span data-stu-id="6a72c-406">Therefore, the time between the end of the generation 0 garbage collection and the end of the generation 2 garbage collection is 4 seconds.</span></span> <span data-ttu-id="6a72c-407">由於 `% Time in GC` 計數器為 20%，因此層代 2 記憶體回收可能花費的最長時間量是 (4 秒 \* 20% = 800 毫秒)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-407">Because the `% Time in GC` counter is 20%, the maximum amount of time the generation 2 garbage collection could have taken is (4 seconds \* 20% = 800ms).</span></span>

- <span data-ttu-id="6a72c-408">或者，您可以使用[記憶體回收 ETW 事件](../../framework/performance/garbage-collection-etw-events.md)來判斷記憶體回收的長度，並分析資訊來判斷記憶體回收的持續時間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-408">Alternatively, you can determine the length of a garbage collection by using [garbage collection ETW events](../../framework/performance/garbage-collection-etw-events.md), and analyze the information to determine the duration of garbage collection.</span></span>

  <span data-ttu-id="6a72c-409">例如，下列資料顯示在非並行記憶體回收期間發生的事件序列。</span><span class="sxs-lookup"><span data-stu-id="6a72c-409">For example, the following data shows an event sequence that occurred during a non-concurrent garbage collection.</span></span>

  ```console
  Timestamp    Event name
  513052        GCSuspendEEBegin_V1
  513078        GCSuspendEEEnd
  513090        GCStart_V1
  517890        GCEnd_V1
  517894        GCHeapStats
  517897        GCRestartEEBegin
  517918        GCRestartEEEnd
  ```

  <span data-ttu-id="6a72c-410">暫止 Managed 執行緒花了 26 微秒 (`GCSuspendEEEnd` – `GCSuspendEEBegin_V1`)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-410">Suspending the managed thread took 26us (`GCSuspendEEEnd` – `GCSuspendEEBegin_V1`).</span></span>

  <span data-ttu-id="6a72c-411">實際的記憶體回收花了 4.8 毫秒 (`GCEnd_V1` – `GCStart_V1`)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-411">The actual garbage collection took 4.8ms (`GCEnd_V1` – `GCStart_V1`).</span></span>

  <span data-ttu-id="6a72c-412">繼續 Managed 執行緒花了 21 微秒 (`GCRestartEEEnd` – `GCRestartEEBegin`)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-412">Resuming the managed threads took 21us (`GCRestartEEEnd` – `GCRestartEEBegin`).</span></span>

  <span data-ttu-id="6a72c-413">下列輸出提供背景記憶體回收的範例，並包含處理序、執行緒和事件欄位。</span><span class="sxs-lookup"><span data-stu-id="6a72c-413">The following output provides an example for background garbage collection, and includes the process, thread, and event fields.</span></span> <span data-ttu-id="6a72c-414">(並非所有資料皆會顯示)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-414">(Not all data is shown.)</span></span>

  ```console
  timestamp(us)    event name            process    thread    event field
  42504385        GCSuspendEEBegin_V1    Test.exe    4372             1
  42504648        GCSuspendEEEnd         Test.exe    4372
  42504816        GCStart_V1             Test.exe    4372        102019
  42504907        GCStart_V1             Test.exe    4372        102020
  42514170        GCEnd_V1               Test.exe    4372
  42514204        GCHeapStats            Test.exe    4372        102020
  42832052        GCRestartEEBegin       Test.exe    4372
  42832136        GCRestartEEEnd         Test.exe    4372
  63685394        GCSuspendEEBegin_V1    Test.exe    4744             6
  63686347        GCSuspendEEEnd         Test.exe    4744
  63784294        GCRestartEEBegin       Test.exe    4744
  63784407        GCRestartEEEnd         Test.exe    4744
  89931423        GCEnd_V1               Test.exe    4372        102019
  89931464        GCHeapStats            Test.exe    4372
  ```

  <span data-ttu-id="6a72c-415">在 42504816 的 `GCStart_V1` 事件表示這是背景記憶體回收，因為最後一個欄位是 `1`。</span><span class="sxs-lookup"><span data-stu-id="6a72c-415">The `GCStart_V1` event at 42504816 indicates that this is a background garbage collection, because the last field is `1`.</span></span> <span data-ttu-id="6a72c-416">這會變成記憶體回收第 </span><span class="sxs-lookup"><span data-stu-id="6a72c-416">This becomes garbage collection No.</span></span> <span data-ttu-id="6a72c-417">102019 號。</span><span class="sxs-lookup"><span data-stu-id="6a72c-417">102019.</span></span>

  <span data-ttu-id="6a72c-418">因為需要先進行暫時記憶體回收，才能開始背景記憶體回收，因此發生 `GCStart` 事件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-418">The `GCStart` event occurs because there is a need for an ephemeral garbage collection before you start a background garbage collection.</span></span> <span data-ttu-id="6a72c-419">這會變成記憶體回收第 </span><span class="sxs-lookup"><span data-stu-id="6a72c-419">This becomes garbage collection No.</span></span> <span data-ttu-id="6a72c-420">102020 號。</span><span class="sxs-lookup"><span data-stu-id="6a72c-420">102020.</span></span>

  <span data-ttu-id="6a72c-421">在 42514170 處，記憶體回收第</span><span class="sxs-lookup"><span data-stu-id="6a72c-421">At 42514170, garbage collection No.</span></span> <span data-ttu-id="6a72c-422">102020 號完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-422">102020 finishes.</span></span> <span data-ttu-id="6a72c-423">Managed 執行緒會在此時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="6a72c-423">The managed threads are restarted at this point.</span></span> <span data-ttu-id="6a72c-424">此步驟會在執行緒 4372，觸發此背景記憶體回收完成。</span><span class="sxs-lookup"><span data-stu-id="6a72c-424">This is completed on thread 4372, which triggered this background garbage collection.</span></span>

  <span data-ttu-id="6a72c-425">在執行緒 4744 上發生擱置。</span><span class="sxs-lookup"><span data-stu-id="6a72c-425">On thread 4744, a suspension occurs.</span></span> <span data-ttu-id="6a72c-426">這是背景記憶體回收唯一必須暫止 Managed 執行緒的時間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-426">This is the only time at which the background garbage collection has to suspend managed threads.</span></span> <span data-ttu-id="6a72c-427">這段期間是大約 99 毫秒 ((63784407-63685394)/1000)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-427">This duration is approximately 99ms ((63784407-63685394)/1000).</span></span>

  <span data-ttu-id="6a72c-428">背景記憶體回收的 `GCEnd` 事件位於 89931423。</span><span class="sxs-lookup"><span data-stu-id="6a72c-428">The `GCEnd` event for the background garbage collection is at 89931423.</span></span> <span data-ttu-id="6a72c-429">這表示背景記憶體回收持續大約 47 秒 ((89931423-42504816)/1000)。</span><span class="sxs-lookup"><span data-stu-id="6a72c-429">This means that the background garbage collection lasted for about 47seconds ((89931423-42504816)/1000).</span></span>

  <span data-ttu-id="6a72c-430">在 Managed 執行緒執行時，您可能看到發生任意數目的暫時記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-430">While the managed threads are running, you can see any number of ephemeral garbage collections occurring.</span></span>

<a name="Triggered"></a>

### <a name="to-determine-what-triggered-a-garbage-collection"></a><span data-ttu-id="6a72c-431">判斷觸發記憶體回收的原因</span><span class="sxs-lookup"><span data-stu-id="6a72c-431">To determine what triggered a garbage collection</span></span>

- <span data-ttu-id="6a72c-432">在已載入 SOS 偵錯工具擴充功能的 WinDbg 或 Visual Studio 偵錯工具中，輸入下列命令以顯示所有執行緒及其呼叫堆疊：</span><span class="sxs-lookup"><span data-stu-id="6a72c-432">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command to show all the threads with their call stacks:</span></span>

  <span data-ttu-id="6a72c-433">**~\*K b**</span><span class="sxs-lookup"><span data-stu-id="6a72c-433">**~\*kb**</span></span>

  <span data-ttu-id="6a72c-434">這個命令會顯示與下列類似的輸出。</span><span class="sxs-lookup"><span data-stu-id="6a72c-434">This command displays output similar to the following.</span></span>

  ```console
  0012f3b0 79ff0bf8 mscorwks!WKS::GCHeap::GarbageCollect
  0012f454 30002894 mscorwks!GCInterface::CollectGeneration+0xa4
  0012f490 79fa22bd fragment_ni!request.Main(System.String[])+0x48
  ```

  <span data-ttu-id="6a72c-435">如果記憶體回收的起因是來自作業系統的記憶體不足通知，則呼叫堆疊會很類似，只除了執行緒是完成項執行緒。</span><span class="sxs-lookup"><span data-stu-id="6a72c-435">If the garbage collection was caused by a low memory notification from the operating system, the call stack is similar, except that the thread is the finalizer thread.</span></span> <span data-ttu-id="6a72c-436">完成項執行緒會收到非同步記憶體偏低通知，並引發記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-436">The finalizer thread gets an asynchronous low memory notification and induces the garbage collection.</span></span>

  <span data-ttu-id="6a72c-437">如果記憶體回收的起因是記憶體配置，則堆疊會如下所示：</span><span class="sxs-lookup"><span data-stu-id="6a72c-437">If the garbage collection was caused by memory allocation, the stack appears as follows:</span></span>

  ```console
  0012f230 7a07c551 mscorwks!WKS::GCHeap::GarbageCollectGeneration
  0012f2b8 7a07cba8 mscorwks!WKS::gc_heap::try_allocate_more_space+0x1a1
  0012f2d4 7a07cefb mscorwks!WKS::gc_heap::allocate_more_space+0x18
  0012f2f4 7a02a51b mscorwks!WKS::GCHeap::Alloc+0x4b
  0012f310 7a02ae4c mscorwks!Alloc+0x60
  0012f364 7a030e46 mscorwks!FastAllocatePrimitiveArray+0xbd
  0012f424 300027f4 mscorwks!JIT_NewArr1+0x148
  000af70f 3000299f fragment_ni!request..ctor(Int32, Single)+0x20c
  0000002a 79fa22bd fragment_ni!request.Main(System.String[])+0x153
  ```

  <span data-ttu-id="6a72c-438">Just-In-Time 協助程式 (`JIT_New*`) 實際上呼叫 `GCHeap::GarbageCollectGeneration`。</span><span class="sxs-lookup"><span data-stu-id="6a72c-438">A just-in-time helper (`JIT_New*`) eventually calls `GCHeap::GarbageCollectGeneration`.</span></span> <span data-ttu-id="6a72c-439">如果您判斷層代 2 記憶體回收起因是配置，則必須判斷層代 2 記憶體回收會回收哪些物件及如何加以避免。</span><span class="sxs-lookup"><span data-stu-id="6a72c-439">If you determine that generation 2 garbage collections are caused by allocations, you must determine which objects are collected by a generation 2 garbage collection and how to avoid them.</span></span> <span data-ttu-id="6a72c-440">也就是您想要判斷層代 2 記憶體回收開始和結束之間的差異，以及造成層代 2 記憶體回收的物件。</span><span class="sxs-lookup"><span data-stu-id="6a72c-440">That is, you want to determine the difference between the start and the end of a generation 2 garbage collection, and the objects that caused the generation 2 collection.</span></span>

  <span data-ttu-id="6a72c-441">例如，在偵錯工具中輸入下列命令以顯示層代 2 記憶體回收的開始：</span><span class="sxs-lookup"><span data-stu-id="6a72c-441">For example, type the following command in the debugger to show the beginning of a generation 2 collection:</span></span>

  <span data-ttu-id="6a72c-442">**!dumpheap –stat**</span><span class="sxs-lookup"><span data-stu-id="6a72c-442">**!dumpheap –stat**</span></span>

  <span data-ttu-id="6a72c-443">範例輸出 (經過刪減以顯示使用最大空間的物件)：</span><span class="sxs-lookup"><span data-stu-id="6a72c-443">Example output (abridged to show the objects that use the most space):</span></span>

  ```console
  79124228    31857      9862328 System.Object[]
  035f0384    25668     11601936 Toolkit.TlkPosition
  00155f80    21248     12256296      Free
  79103b6c   297003     13068132 System.Threading.ReaderWriterLock
  7a747ad4   708732     14174640 System.Collections.Specialized.HybridDictionary
  7a747c78   786498     15729960 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary
  035f0ee4    89192     38887712 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  7912c444    91616     71887080 System.Double[]
  791242ec    32451     82462728 System.Collections.Hashtable+bucket[]
  790fa3e0  2459154    112128436 System.String
  Total 6471774 objects
  ```

  <span data-ttu-id="6a72c-444">在層代 2 結束時重複執行命令：</span><span class="sxs-lookup"><span data-stu-id="6a72c-444">Repeat the command at the end of generation 2:</span></span>

  <span data-ttu-id="6a72c-445">**!dumpheap –stat**</span><span class="sxs-lookup"><span data-stu-id="6a72c-445">**!dumpheap –stat**</span></span>

  <span data-ttu-id="6a72c-446">範例輸出 (經過刪減以顯示使用最大空間的物件)：</span><span class="sxs-lookup"><span data-stu-id="6a72c-446">Example output (abridged to show the objects that use the most space):</span></span>

  ```console
  79124228    26648      9314256 System.Object[]
  035f0384    25668     11601936 Toolkit.TlkPosition
  79103b6c   296770     13057880 System.Threading.ReaderWriterLock
  7a747ad4   708730     14174600 System.Collections.Specialized.HybridDictionary
  7a747c78   786497     15729940 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary
  00155f80    13806     34007212      Free
  035f0ee4    89187     38885532 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  791242ec    32370     82359768 System.Collections.Hashtable+bucket[]
  790fa3e0  2440020    111341808 System.String
  Total 6417525 objects
  ```

  <span data-ttu-id="6a72c-447">`double[]` 物件從輸出結束消失，這表示它們已被回收。</span><span class="sxs-lookup"><span data-stu-id="6a72c-447">The `double[]` objects disappeared from the end of the output, which means that they were collected.</span></span> <span data-ttu-id="6a72c-448">這些物件大約 70 MB。</span><span class="sxs-lookup"><span data-stu-id="6a72c-448">These objects account for approximately 70 MB.</span></span> <span data-ttu-id="6a72c-449">剩餘的物件變更不多。</span><span class="sxs-lookup"><span data-stu-id="6a72c-449">The remaining objects did not change much.</span></span> <span data-ttu-id="6a72c-450">因此，這些 `double[]` 物件便是這個層代 2 記憶體回收發生的原因。</span><span class="sxs-lookup"><span data-stu-id="6a72c-450">Therefore, these `double[]` objects were the reason why this generation 2 garbage collection occurred.</span></span> <span data-ttu-id="6a72c-451">您的下一個步驟是判斷 `double[]` 物件為何出現，以及其終止原因。</span><span class="sxs-lookup"><span data-stu-id="6a72c-451">Your next step is to determine why the `double[]` objects are there and why they died.</span></span> <span data-ttu-id="6a72c-452">您可以要求程式碼開發人員這些物件的來源，或者您可以使用 **gcroot** 命令。</span><span class="sxs-lookup"><span data-stu-id="6a72c-452">You can ask the code developer where these objects came from, or you can use the **gcroot** command.</span></span>

<a name="HighCPU"></a>

### <a name="to-determine-whether-high-cpu-usage-is-caused-by-garbage-collection"></a><span data-ttu-id="6a72c-453">判斷高 CPU 使用量是否由於記憶體回收所造成</span><span class="sxs-lookup"><span data-stu-id="6a72c-453">To determine whether high CPU usage is caused by garbage collection</span></span>

- <span data-ttu-id="6a72c-454">相互關聯 `% Time in GC` 記憶體效能計數器值與處理序時間。</span><span class="sxs-lookup"><span data-stu-id="6a72c-454">Correlate the `% Time in GC` memory performance counter value with the process time.</span></span>

  <span data-ttu-id="6a72c-455">如果 `% Time in GC` 值與處理序時間同時升高，則記憶體回收便造成高 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="6a72c-455">If the `% Time in GC` value spikes at the same time as process time, garbage collection is causing a high CPU usage.</span></span> <span data-ttu-id="6a72c-456">否則，請針對應用程式進行程式碼剖析，尋找發生高使用量的地方。</span><span class="sxs-lookup"><span data-stu-id="6a72c-456">Otherwise, profile the application to find where the high usage is occurring.</span></span>

## <a name="see-also"></a><span data-ttu-id="6a72c-457">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6a72c-457">See also</span></span>

- [<span data-ttu-id="6a72c-458">記憶體回收</span><span class="sxs-lookup"><span data-stu-id="6a72c-458">Garbage Collection</span></span>](index.md)
